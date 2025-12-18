# Admin Creates User Accounts

**Story ID:** US-0.3.3  
**Epic:** 0.3 - Authentication & Access Control  
**Personas:** HR Admin, Super Admin

---

## User Story

> **As an** HR Admin or Super Admin,  
> **I want to** create user accounts and invite team members,  
> **So that** new employees can access the system.

---

## Business Requirement/Logic

Admins can add new team members by sending email invitations. New users receive temporary credentials and must set their own password on first login.

**Key Business Rules:**
- Only users with `employee.create` permission can create accounts
- Admin can only assign roles at their level or below
- Temporary password expires in 72 hours
- New user status starts as "pending"
- Status changes to "active" after first password change
- Email must be unique across the entire system
- Resend invitation resets the 72-hour expiry

---

## Acceptance Criteria

### Scenario 1: Successfully Create User Account

**Given**
- Admin is logged in with `employee.create` permission
- Admin is on Team → Members page

**When**
- Admin clicks "Add Team Member"
- Admin enters valid email address
- Admin enters full name
- Admin selects role(s)
- Admin clicks "Send Invitation"

**Then**
- System creates user account with status "pending"
- System generates temporary password
- System sends invitation email with credentials
- System shows success message "Invitation sent to {email}"
- New user appears in list with "Pending" badge
- Audit log records the action

---

### Scenario 2: Invitee First Login - Password Change

**Given**
- New user has received invitation email
- Temporary password has not expired

**When**
- User clicks login link in email
- User enters email and temporary password
- User clicks "Sign In"

**Then**
- System validates temp password
- System detects first login
- System redirects to "Set Password" page
- User enters new password
- User confirms new password
- System updates password
- System changes status to "active"
- System redirects to Dashboard

---

### Scenario 3: Email Already Registered

**Given**
- Admin is on Add Team Member modal

**When**
- Admin enters email that already exists in system
- Admin attempts to submit

**Then**
- System shows error "A user with this email already exists"
- Form is not submitted
- Admin can enter different email

---

### Scenario 4: Admin Lacks Permission to Assign Role

**Given**
- Admin is on Add Team Member modal
- Admin's permission level is lower than selected role

**When**
- Admin tries to assign a role above their level

**Then**
- Role is not shown in dropdown (filtered out)
- OR system shows error "You don't have permission to assign this role"
- Form is not submitted

---

### Scenario 5: Temporary Password Expired

**Given**
- New user was invited more than 72 hours ago
- User has not logged in yet

**When**
- User tries to login with temp password

**Then**
- System shows error "Invitation expired. Ask admin to resend"
- User cannot login
- Admin can use "Resend" option

---

### Scenario 6: Resend Invitation

**Given**
- Admin is on Team Members list
- A user has "Pending" status

**When**
- Admin clicks "Resend" on the pending user

**Then**
- System generates new temporary password
- System resets 72-hour expiry timer
- System sends new invitation email
- System shows message "Invitation resent to {email}"

---

### Scenario 7: Email Delivery Failed

**Given**
- Admin is creating a new user

**When**
- User account is created successfully
- Email service fails to send

**Then**
- System shows warning "Invitation created but email failed. Use 'Resend' option"
- User is created with status "pending"
- Admin can manually resend invitation

---

### Scenario 8: Create User with Department Assignment

**Given**
- Admin is on Add Team Member modal
- Departments exist in the system

**When**
- Admin fills required fields
- Admin selects a department
- Admin clicks "Send Invitation"

**Then**
- User is created with department assignment
- User will see their department on profile
- User appears in department's member list

---

### Scenario 9: First Login Password Doesn't Meet Requirements

**Given**
- New user is on "Set Password" page after first login

**When**
- User enters password that doesn't meet requirements
- User clicks "Set Password"

**Then**
- System shows error with specific requirement missing
- Form is not submitted
- User must enter stronger password

---

### Scenario 10: Cancel User Invitation

**Given**
- Admin is on Team Members list
- A user has "Pending" status

**When**
- Admin clicks "Cancel Invitation" on the pending user
- Admin confirms cancellation

**Then**
- System marks invitation as cancelled
- Temporary password is invalidated
- User is removed from list (or shown as "Cancelled")
- User cannot login with invitation credentials

---

## UI/UX Notes

**Screens Involved:**
1. Team Members List (`/team`)
2. Add Team Member Modal
3. First Login - Set Password Page

**Key UI Elements:**
- **Email Input:** Required, with format validation
- **Name Input:** Required, auto-capitalizes
- **Role Selector:** Multi-select dropdown, filtered by admin's permissions
- **Department Selector:** Optional dropdown
- **Send Invitation Button:** Primary action
- **Pending Badge:** Yellow badge on list items
- **Resend Link:** Available for pending users
- **Cancel Link:** Available for pending users

**List View Columns:**
- Name
- Email
- Role(s)
- Department
- Status (Active/Pending/Inactive)
- Invited Date
- Actions (Resend/Cancel for pending)
