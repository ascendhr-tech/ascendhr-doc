# Password Management

**Story ID:** US-0.3.2  
**Epic:** 0.3 - Authentication & Access Control  
**Personas:** Employee, HR Admin, Super Admin

---

## User Story

> **As a** user,  
> **I want to** reset my forgotten password or change my current password,  
> **So that** I can regain access to my account or maintain security.

---

## Business Requirement/Logic

Users can manage their passwords through two flows: forgot password (for locked-out users) and change password (for logged-in users).

**Key Business Rules:**
- Reset token expires in 1 hour
- Reset token is single-use (invalidated after use)
- Password requirements: min 8 chars, 1 uppercase, 1 number
- New password cannot be same as current password
- All active sessions invalidated on password reset
- Password history: cannot reuse last 3 passwords
- Security: same success message shown whether email exists or not (forgot password)

---

## Acceptance Criteria

### Scenario 1: Successful Password Reset Request

**Given**
- User has a registered account
- User is on the forgot password page

**When**
- User enters their registered email
- User clicks "Send Reset Link"

**Then**
- System generates secure reset token (expires in 1 hour)
- System sends email with reset link
- System shows message "Check your email for reset instructions"
- Email contains link in format `/reset-password?token={token}`

---

### Scenario 2: Successful Password Reset

**Given**
- User has received reset email
- Reset token is valid and not expired
- User is on the reset password page

**When**
- User enters new password meeting requirements
- User confirms new password (matching)
- User clicks "Reset Password"

**Then**
- System updates password in database
- System invalidates the reset token
- System invalidates all existing sessions
- System redirects to login page
- User sees message "Password reset successfully. Please log in."

---

### Scenario 3: Successful Password Change (Logged In)

**Given**
- User is logged in
- User is on Settings → Security page

**When**
- User enters correct current password
- User enters new password (different from current)
- User confirms new password
- User clicks "Update Password"

**Then**
- System verifies current password
- System updates password in database
- System optionally invalidates other sessions
- User sees message "Password updated successfully"
- User remains logged in on current session

---

### Scenario 4: Reset Token Expired

**Given**
- User has a reset token older than 1 hour

**When**
- User clicks the reset link in email

**Then**
- System shows error "This link has expired. Please request a new one"
- System shows link to forgot password page
- Token is marked as expired

---

### Scenario 5: Reset Token Already Used

**Given**
- User has already used their reset token

**When**
- User clicks the same reset link again

**Then**
- System shows error "This link has already been used"
- System shows link to forgot password page

---

### Scenario 6: Password Too Weak

**Given**
- User is on reset password or change password page

**When**
- User enters password less than 8 characters
- OR password without uppercase letter
- OR password without number

**Then**
- System shows error "Password must be at least 8 characters with 1 uppercase and 1 number"
- Form is not submitted
- Password strength indicator shows "Weak"

---

### Scenario 7: Passwords Don't Match

**Given**
- User is on reset password or change password page

**When**
- User enters new password
- User enters different password in confirm field

**Then**
- System shows error "Passwords do not match"
- Confirm field is highlighted
- Form is not submitted

---

### Scenario 8: Current Password Incorrect (Change Password)

**Given**
- User is logged in on Settings → Security
- User is changing their password

**When**
- User enters wrong current password
- User clicks "Update Password"

**Then**
- System shows error "Current password is incorrect"
- Current password field is cleared
- User can retry

---

### Scenario 9: New Password Same as Current

**Given**
- User is on reset password or change password page

**When**
- User enters the same password as their current password

**Then**
- System shows error "New password must be different from current password"
- Form is not submitted

---

### Scenario 10: Email Not Found (Security - Silent Success)

**Given**
- User is on forgot password page
- No account exists with entered email

**When**
- User enters non-existent email
- User clicks "Send Reset Link"

**Then**
- System shows same success message "Check your email for reset instructions"
- No email is sent (but user doesn't know this)
- This prevents user enumeration attacks

---

## UI/UX Notes

**Screens Involved:**
1. Forgot Password Page (`/forgot-password`)
2. Reset Password Page (`/reset-password?token=...`)
3. Security Settings Page (`/settings/security`)
4. Change Password Modal/Form

**Key UI Elements:**
- **Email Input:** On forgot password page
- **Password Input:** With strength indicator (Weak/Medium/Strong)
- **Confirm Password:** With match indicator
- **Password Requirements:** Shown below password field
- **Show/Hide Toggle:** Eye icon to toggle password visibility
- **Submit Button:** Disabled until form is valid

**Password Strength Indicator:**
- Weak (red): < 8 chars or missing requirements
- Medium (yellow): Meets basic requirements
- Strong (green): 12+ chars with special characters
