# User Login/Logout

**Story ID:** US-0.3.1  
**Epic:** 0.3 - Authentication & Access Control  
**Personas:** Employee, HR Admin, Super Admin

---

## User Story

> **As an** employee,  
> **I want to** login and logout securely,  
> **So that** I can access my personal dashboard and data.

---

## Business Requirement/Logic

Users must authenticate before accessing any protected resources. The system uses JWT tokens for stateless authentication.

**Key Business Rules:**
- JWT access token expires in 15 minutes
- Refresh token expires in 7 days (30 days with "Remember Me")
- Maximum 5 failed login attempts before account lockout
- Account unlocks after 30 minutes or via password reset
- Rate limiting: max 5 login attempts per minute per IP
- Session persists across browser restarts if "Remember Me" is checked
- All sessions invalidated on password change

---

## Acceptance Criteria

### Scenario 1: Successful Login

**Given**
- User has a verified account
- User is on the login page

**When**
- User enters valid email and password
- User clicks "Sign In"

**Then**
- System generates JWT access token and refresh token
- System stores tokens in httpOnly cookies
- System redirects user to Dashboard
- User sees welcome message "Welcome back, {name}!"

---

### Scenario 2: Successful Logout

**Given**
- User is logged in
- User is on any page of the application

**When**
- User clicks avatar in header
- User clicks "Logout" in dropdown
- User confirms logout

**Then**
- System invalidates tokens on server
- System clears all cookies
- System redirects to login page
- User sees message "You have been logged out"

---

### Scenario 3: Invalid Email Format

**Given**
- User is on the login page

**When**
- User enters email without @ symbol or invalid format
- User attempts to submit

**Then**
- System shows error "Please enter a valid email address"
- Form is not submitted
- Focus remains on email field

---

### Scenario 4: Account Not Found

**Given**
- User is on the login page
- No account exists with the entered email

**When**
- User enters unregistered email
- User enters any password
- User clicks "Sign In"

**Then**
- System shows error "No account found with this email"
- Password field is cleared
- User can try again

---

### Scenario 5: Wrong Password

**Given**
- User is on the login page
- Account exists with status "active"

**When**
- User enters correct email but wrong password
- User clicks "Sign In"

**Then**
- System increments failed attempt counter
- System shows error "Incorrect password. {remaining} attempts remaining"
- Password field is cleared

---

### Scenario 6: Account Locked After 5 Failed Attempts

**Given**
- User has failed login 4 times
- User is on the login page

**When**
- User enters wrong password again (5th attempt)

**Then**
- System locks the account for 30 minutes
- System shows error "Account locked. Please reset your password or contact support"
- Login form shows "Forgot Password" link prominently
- User cannot attempt login until timeout or password reset

---

### Scenario 7: Email Not Verified

**Given**
- User has registered but not verified email
- User is on the login page

**When**
- User enters correct credentials

**Then**
- System shows error "Please verify your email first"
- System shows "Resend verification email" link
- User cannot access dashboard until verified

---

### Scenario 8: Session Expired During Use

**Given**
- User is logged in
- Access token has expired
- Refresh token is still valid

**When**
- User makes a request to the server

**Then**
- System automatically refreshes access token
- Request completes successfully
- User session continues without interruption

---

### Scenario 9: Refresh Token Expired

**Given**
- User was logged in
- Both access token and refresh token have expired

**When**
- User attempts to access any protected page

**Then**
- System redirects to login page
- System shows message "Your session has expired. Please login again"
- User must re-authenticate

---

### Scenario 10: Remember Me - Session Persistence

**Given**
- User is on the login page
- "Remember Me" checkbox is available

**When**
- User enters valid credentials
- User checks "Remember Me"
- User clicks "Sign In"

**Then**
- System generates refresh token with 30-day expiry (instead of 7 days)
- User stays logged in across browser restarts
- User stays logged in for up to 30 days of inactivity

---

## UI/UX Notes

**Screens Involved:**
1. Login Page (`/login`)
2. Dashboard (redirect target)
3. User dropdown menu (header component)

**Key UI Elements:**
- **Email Input:** Standard text input with email validation
- **Password Input:** Masked input with show/hide toggle
- **Remember Me:** Checkbox below password field
- **Sign In Button:** Primary action button, disabled during submission
- **Forgot Password Link:** Below form, links to password reset
- **Social Login (Future):** Google/SSO buttons (optional)

**Error States:**
- Inline error messages below respective fields
- Toast notification for global errors
- Shake animation on validation failure
