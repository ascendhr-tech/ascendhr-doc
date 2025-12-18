# Auth Middleware & Guards (Technical)

**Story ID:** US-0.3.4  
**Epic:** 0.3 - Authentication & Access Control  
**Personas:** Developer (Technical Story)

---

## User Story

> **As a** developer,  
> **I want** reusable authentication middleware and route guards,  
> **So that** all protected routes are secured consistently.

---

## Business Requirement/Logic

All API routes and frontend pages must be protected by consistent authentication and authorization checks. The system uses JWT tokens with automatic refresh capability.

**Key Technical Requirements:**
- JWT verification on every protected API request
- Role/Permission-based access control
- Multi-tenant isolation (company-scoped data)
- Automatic token refresh (transparent to user)
- Consistent error responses (401/403)
- Frontend auth context for UI state

---

## Acceptance Criteria

### Scenario 1: Valid Token Passes Middleware

**Given**
- User has a valid, non-expired access token
- User makes request to protected API endpoint

**When**
- Request reaches auth middleware

**Then**
- Middleware validates JWT signature
- Middleware checks token expiration
- Middleware extracts user context (userId, companyId, roles)
- Request proceeds to handler with user context attached
- Handler can access `req.user` object

---

### Scenario 2: Expired Access Token - Auto Refresh

**Given**
- User's access token has expired
- User's refresh token is still valid
- User makes request to protected endpoint

**When**
- Access token validation fails with "expired"

**Then**
- Middleware attempts to refresh using refresh token
- New access token is generated
- New access token is set in httpOnly cookie
- Original request is retried with new token
- User experiences no interruption

---

### Scenario 3: Invalid Token - Rejected

**Given**
- User has an invalid or tampered token
- User makes request to protected API endpoint

**When**
- Request reaches auth middleware

**Then**
- Middleware rejects the request
- Response returns 401 Unauthorized
- Response body: `{ "error": "Invalid authentication token" }`
- User is redirected to login on frontend

---

### Scenario 4: Missing Token - Rejected

**Given**
- Request has no access token in cookies/headers
- Request is made to protected endpoint

**When**
- Request reaches auth middleware

**Then**
- Middleware rejects the request
- Response returns 401 Unauthorized
- Response body: `{ "error": "Authentication required" }`
- Frontend redirects to login page

---

### Scenario 5: Insufficient Permissions - Forbidden

**Given**
- User has valid authentication
- User's role lacks required permission for endpoint
- Endpoint requires `employee.delete` permission
- User only has `employee.read` permission

**When**
- User makes request to delete endpoint

**Then**
- Middleware validates token (passes)
- Permission check fails
- Response returns 403 Forbidden
- Response body: `{ "error": "You do not have permission to perform this action" }`
- Frontend shows 403 page

---

### Scenario 6: Multi-tenant Data Isolation

**Given**
- User is authenticated with Company A
- User attempts to access data belonging to Company B

**When**
- Request includes ID from Company B
- Request reaches data access layer

**Then**
- Middleware extracts companyId from token
- All database queries are filtered by companyId
- Request returns 404 (not 403, to prevent enumeration)
- User cannot access any cross-tenant data

---

### Scenario 7: Frontend Auth Context - Logged In

**Given**
- User has valid session
- Frontend app is loaded

**When**
- App initializes AuthContext

**Then**
- Context loads user profile from token/API
- Context exposes: `user`, `isAuthenticated`, `permissions`, `loading`
- Components can use `useAuth()` hook
- Protected routes render correctly

---

### Scenario 8: Frontend Auth Context - Not Authenticated

**Given**
- User is not logged in
- User navigates to protected route

**When**
- ProtectedRoute component checks auth state

**Then**
- `isAuthenticated` returns false
- User is redirected to `/login`
- Original URL is stored for post-login redirect
- Protected content is not rendered

---

### Scenario 9: Token Refresh Failed - Full Logout

**Given**
- User's access token is expired
- User's refresh token is also expired or invalid

**When**
- Middleware attempts auto-refresh

**Then**
- Refresh fails
- All cookies are cleared
- User is redirected to login page
- Session expired modal shown: "Your session has expired. Please login again"

---

### Scenario 10: Permission Check with AND/OR Logic

**Given**
- Endpoint requires multiple permissions

**When**
- Endpoint is configured with `permissions: ['employee.read', 'employee.update']` (AND)
- OR endpoint is configured with `anyPermission: ['admin.all', 'employee.update']` (OR)

**Then**
- AND: User must have ALL listed permissions
- OR: User must have AT LEAST ONE permission
- Correct check is applied based on configuration

---

## UI/UX Notes

**Screens Involved:**
1. 403 Forbidden Page (`/403`)
2. Session Expired Modal (overlay)

**Key UI Elements:**
- **403 Page:** Shows friendly error message, link to dashboard
- **Session Modal:** Overlay that appears when session expires
- **Loading State:** Skeleton/spinner while auth is checking

**API Response Formats:**
```json
// 401 Unauthorized
{
  "error": "Authentication required",
  "code": "AUTH_REQUIRED"
}

// 403 Forbidden  
{
  "error": "You do not have permission to perform this action",
  "code": "PERMISSION_DENIED",
  "required": "employee.delete"
}
```

**Auth Context Interface:**
```typescript
interface AuthContext {
  user: User | null;
  isAuthenticated: boolean;
  isLoading: boolean;
  permissions: string[];
  hasPermission: (permission: string) => boolean;
  hasAnyPermission: (permissions: string[]) => boolean;
  login: (credentials: Credentials) => Promise<void>;
  logout: () => Promise<void>;
  refresh: () => Promise<void>;
}
```
