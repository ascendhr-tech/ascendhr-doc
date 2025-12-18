# Foundation + Auth - User Stories

**Epic:** 0.1, 0.2, 0.3  
**Version:** 1.0  
**Created:** December 16, 2024  
**Purpose:** User stories for UX flow design and developer implementation

---

## Overview

| Epic | Scope | Estimate |
|------|-------|----------|
| Epic 0.1 | Project Infrastructure Setup | 3 man-days |
| Epic 0.2 | Core Database Design | 2 man-days |
| Epic 0.3 | Authentication & Access Control | 5 man-days |
| **Total** | | **10 man-days** |

> **Note:** Epic 0.1 and 0.2 are technical infrastructure tasks without user-facing screens. This document focuses on Epic 0.3 user stories.

---

## User Personas

| Persona | Role | Key Actions |
|---------|------|-------------|
| **Employee** | Any authenticated user | Login, logout, reset password, change password |
| **HR Admin** | HR Staff (Scout role) | Create user accounts, manage team members |
| **Super Admin** | Club Owner | Full access, system configuration |

---

## Technical Prerequisites

### Epic 0.1: Project Infrastructure Setup

| ID | Task | Estimate |
|----|------|----------|
| TASK-0.1.1 | Git repo + branching strategy | 0.25d |
| TASK-0.1.2 | Next.js + TypeScript + MUI + Tailwind setup | 0.5d |
| TASK-0.1.3 | Prisma/Drizzle ORM setup | 0.25d |
| TASK-0.1.4 | CI/CD pipeline (GitHub Actions) | 0.5d |
| TASK-0.1.5 | Docker setup | 0.5d |
| TASK-0.1.6 | Environment configs | 0.25d |
| TASK-0.1.7 | ESLint + Prettier config | 0.25d |
| TASK-0.1.8 | Vercel/Railway deployment setup | 0.5d |

### Epic 0.2: Core Database Design

| ID | Task | Estimate |
|----|------|----------|
| TASK-0.2.1 | ERD design for Phase 0-1 | 0.5d |
| TASK-0.2.2 | Users + Roles + Permissions migrations | 0.5d |
| TASK-0.2.3 | Employees + Hierarchy migration | 0.25d |
| TASK-0.2.4 | Departments + Positions migration | 0.25d |
| TASK-0.2.5 | Consent + Audit logs migration | 0.25d |
| TASK-0.2.6 | Seed data (roles, permissions) | 0.25d |

---

## US-0.3.1: User Login/Logout

> **As an** employee,  
> **I want to** login and logout securely,  
> **So that** I can access my personal dashboard and data.

### Scenario
An employee navigates to the AscendHR application and needs to authenticate to access their dashboard. After completing their work, they can securely logout.

### Preconditions
- User account exists in the system
- User has verified their email
- User knows their credentials (email + password)

### Main Flow - Login

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Navigate to `/login` | Display login form with email/password fields |
| 2 | Enter email address | Validate email format in real-time |
| 3 | Enter password | Show password strength (masked) |
| 4 | Click "Sign In" button | Validate credentials against database |
| 5 | - | Generate JWT access token + refresh token |
| 6 | - | Store tokens in httpOnly cookies |
| 7 | - | Redirect to Dashboard |
| 8 | - | Display welcome message: "Welcome back, {name}!" |

### Main Flow - Logout

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Click user avatar in header | Display dropdown menu |
| 2 | Click "Logout" | Confirm logout action |
| 3 | Confirm logout | Invalidate tokens on server |
| 4 | - | Clear cookies |
| 5 | - | Redirect to login page |
| 6 | - | Display message: "You have been logged out" |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 4a | Invalid email format | Show error: "Please enter a valid email address" |
| 4b | Account not found | Show error: "No account found with this email" |
| 4c | Wrong password | Show error: "Incorrect password. {attempts} attempts remaining" |
| 4d | Account locked (5+ failures) | Show error: "Account locked. Please reset your password or contact support" |
| 4e | Email not verified | Show error: "Please verify your email first" with resend link |
| 7a | Session expired | Redirect to login with message: "Your session has expired. Please login again" |

### Screens
1. Login Page (`/login`)
2. Dashboard (redirect target)
3. User dropdown menu (logout trigger)

### Tasks
| ID | Task | Est. |
|----|------|------|
| TASK-0.3.1.1 | Login form UI (MUI) | 0.25d |
| TASK-0.3.1.2 | JWT access + refresh token implementation | 0.5d |
| TASK-0.3.1.3 | Login API with rate limiting | 0.25d |
| TASK-0.3.1.4 | Logout with token invalidation | 0.25d |
| TASK-0.3.1.5 | Session persistence (remember me) | 0.25d |

---

## US-0.3.2: Password Management

> **As a** user,  
> **I want to** reset my forgotten password or change my current password,  
> **So that** I can regain access to my account or maintain security.

### Scenario A: Forgot Password
A user has forgotten their password and needs to reset it via email verification.

### Scenario B: Change Password
A logged-in user wants to change their password from account settings.

### Preconditions (Forgot)
- User has a registered account
- User has access to their registered email

### Preconditions (Change)
- User is logged in
- User knows their current password

### Main Flow - Forgot Password

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Click "Forgot Password?" on login page | Navigate to forgot password page |
| 2 | Enter registered email | Validate email format |
| 3 | Click "Send Reset Link" | Check if email exists in database |
| 4 | - | Generate secure reset token (expires in 1 hour) |
| 5 | - | Send email with reset link |
| 6 | - | Display message: "Check your email for reset instructions" |
| 7 | Click link in email | Validate token, navigate to reset page |
| 8 | Enter new password | Validate password strength (min 8 chars, 1 uppercase, 1 number) |
| 9 | Confirm new password | Validate passwords match |
| 10 | Click "Reset Password" | Update password in database, invalidate all existing tokens |
| 11 | - | Invalidate reset token |
| 12 | - | Redirect to login with success message |

### Main Flow - Change Password

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Navigate to Settings → Security | Display security settings page |
| 2 | Click "Change Password" | Display change password form |
| 3 | Enter current password | Validate current password |
| 4 | Enter new password | Validate password strength |
| 5 | Confirm new password | Validate passwords match |
| 6 | Click "Update Password" | Update password in database |
| 7 | - | Invalidate other sessions (optional) |
| 8 | - | Display success message: "Password updated successfully" |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 3a | Email not found | Show same success message (security, don't reveal if email exists) |
| 7a | Token expired | Show error: "This link has expired. Please request a new one" |
| 7b | Token already used | Show error: "This link has already been used" |
| 8a | Password too weak | Show error: "Password must be at least 8 characters with 1 uppercase and 1 number" |
| 9a | Passwords don't match | Show error: "Passwords do not match" |
| 3b (Change) | Current password wrong | Show error: "Current password is incorrect" |
| 4b (Change) | New password same as current | Show error: "New password must be different from current password" |

### Screens
1. Forgot Password Page (`/forgot-password`)
2. Reset Password Page (`/reset-password?token=...`)
3. Security Settings Page (`/settings/security`)
4. Change Password Modal/Form

### Tasks
| ID | Task | Est. |
|----|------|------|
| TASK-0.3.2.1 | Password reset request form | 0.25d |
| TASK-0.3.2.2 | Reset token generation + email | 0.5d |
| TASK-0.3.2.3 | Password reset form + API | 0.5d |
| TASK-0.3.2.4 | Change password (logged in) | 0.25d |

---

## US-0.3.3: Admin Creates User Accounts

> **As an** HR Admin or Super Admin,  
> **I want to** create user accounts and invite team members,  
> **So that** new employees can access the system.

### Scenario
An HR Admin needs to add a new employee to the system. The system creates an account and sends an invitation email with a temporary password.

### Preconditions
- Admin is logged in with `employee.create` permission
- New user's email is not already registered

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Navigate to Team → Members | Display team members list |
| 2 | Click "Add Team Member" | Open create user modal/form |
| 3 | Enter email address | Validate email format, check not already registered |
| 4 | Enter full name | Validate name (required) |
| 5 | Select role(s) | Display available roles based on admin's permissions |
| 6 | Select department (optional) | Show department dropdown |
| 7 | Click "Send Invitation" | Create user account with status "pending" |
| 8 | - | Generate temporary password |
| 9 | - | Send invitation email with credentials |
| 10 | - | Display success: "Invitation sent to {email}" |
| 11 | - | Add user to list with "Pending" status badge |

### Main Flow - First Login (Invitee)

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Receive invitation email | Email contains login link + temp password |
| 2 | Click login link | Navigate to login page |
| 3 | Enter email and temp password | Validate credentials |
| 4 | - | Detect first login, redirect to password change |
| 5 | Enter new password | Validate password strength |
| 6 | Confirm new password | Validate match |
| 7 | Click "Set Password" | Update password, change status to "active" |
| 8 | - | Redirect to Dashboard |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 3a | Email already registered | Show error: "A user with this email already exists" |
| 5a | No roles available | Show error: "You don't have permission to assign roles" |
| 9a | Email delivery fails | Show warning: "Invitation created but email failed. Use 'Resend' option" |
| 3b (Invite) | Temp password expired (72h) | Show error: "Invitation expired. Ask admin to resend" |

### Screens
1. Team Members List (`/team`)
2. Add Team Member Modal
3. First Login - Change Password Page

### Tasks
| ID | Task | Est. |
|----|------|------|
| TASK-0.3.3.1 | Create user form (admin) | 0.25d |
| TASK-0.3.3.2 | Email invitation with temp password | 0.5d |
| TASK-0.3.3.3 | First login password change | 0.25d |

---

## US-0.3.4: Auth Middleware & Guards (Technical)

> **As a** developer,  
> **I want** reusable authentication middleware and route guards,  
> **So that** all protected routes are secured consistently.

### Scenario
Technical implementation of JWT verification and permission checking across all API routes and frontend pages.

### Technical Requirements

#### Backend Middleware
1. **JWT Verification**
   - Validate access token on every protected API request
   - Check token expiration
   - Extract user context (userId, companyId, roles)

2. **Role/Permission Checking**
   - Verify user has required permission for the endpoint
   - Support multiple permission checks (AND/OR)
   - Return 403 Forbidden if unauthorized

3. **Company Isolation (Multi-tenant)**
   - Extract companyId from token
   - Apply company filter to all queries
   - Prevent cross-tenant data access

#### Frontend Guards
1. **Auth Context**
   - Store user state (logged in, permissions, profile)
   - Handle token refresh automatically
   - Clear state on logout

2. **Protected Routes**
   - HOC or wrapper for protected pages
   - Redirect to login if not authenticated
   - Show 403 page if unauthorized

### Screens
- 403 Forbidden Page
- Session Expired Modal

### Tasks
| ID | Task | Est. |
|----|------|------|
| TASK-0.3.4.1 | JWT verification middleware | 0.25d |
| TASK-0.3.4.2 | Role/Permission checking middleware | 0.5d |
| TASK-0.3.4.3 | Frontend auth context + hooks | 0.25d |

---

## Summary

| Story | Description | Estimate | Screens |
|-------|-------------|----------|---------|
| US-0.3.1 | User Login/Logout | 1.5d | Login, Dashboard, Logout dropdown |
| US-0.3.2 | Password Management | 1.5d | Forgot, Reset, Settings/Security |
| US-0.3.3 | Admin Creates Users | 1d | Team list, Add modal, First-login |
| US-0.3.4 | Auth Middleware | 1d | 403 page, Session modal |
| **Total** | | **5 days** | |

---

## Output Chain

```
This Document (PRD)
     ↓
UX Agent (ascendhr-ux.md)
     → Creates Mermaid.js flow diagrams
     ↓
UI Designer Agent
     → Creates HTML mockups
     ↓
Developer implements React/Next.js
```
