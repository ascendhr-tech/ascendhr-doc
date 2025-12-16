# Register Account (Owner Sign Up)

**Story ID:** US-0.0.1  
**Epic:** 0.0 - Football Club Setup  
**Persona:** Club Owner

---

## User Story

> **As a** Club Owner,  
> **I want to** create an account on the platform,  
> **So that** I can start my journey to build my squad.

---

## Business Requirement/Logic

เจ้าของธุรกิจต้องการสมัครใช้งาน AscendHR เพื่อจัดการทีมงานของตนเอง ระบบต้องรองรับการลงทะเบียนแบบ self-service และยืนยันตัวตนผ่าน email

**Key Business Rules:**
- Email ต้องไม่ซ้ำกับผู้ใช้ที่มีอยู่ในระบบ
- Password ต้องมีความปลอดภัย (อย่างน้อย 8 ตัวอักษร)
- ต้องยืนยัน email ก่อนเข้าใช้งาน
- Verification link มีอายุ 24 ชั่วโมง
- หลังยืนยัน email สำเร็จ, redirect ไปหน้า "Create Your Club"

---

## Acceptance Criteria

### Scenario 1: Successfully Register Account

**Given**
- User is on the landing page
- User has a valid email address not registered in the system

**When**
- User clicks "Start Your Journey" button
- User fills in name, email, and password (min 8 characters)
- User clicks "Create Account"
- User receives verification email
- User clicks the verification link in the email

**Then**
- System creates user account in pending state
- System sends verification email with secure link
- System shows "Check your email" message
- After clicking link, system activates the account
- System redirects user to "Create Your Club" wizard

---

### Scenario 2: Email Already Registered

**Given**
- User is on the registration form
- Email "john@company.com" is already registered in the system

**When**
- User enters "john@company.com" in the email field
- User attempts to submit the form

**Then**
- System shows error "Email already in use. Login instead?"
- System provides link to login page
- Registration is not processed

---

### Scenario 3: Password Too Weak

**Given**
- User is on the registration form
- User has filled in name and email

**When**
- User enters a password with less than 8 characters
- User attempts to submit

**Then**
- System shows error "Password must be at least 8 characters"
- Form remains open for correction
- Submit button is disabled until password is valid

---

### Scenario 4: Verification Link Expired

**Given**
- User has registered but not verified email
- Verification link is older than 24 hours

**When**
- User clicks the expired verification link

**Then**
- System shows error "Verification link has expired"
- System displays "Resend verification email" button
- User can request a new verification email

---

## UI/UX Notes

**Screens Involved:**
1. Landing Page (with "Start Your Journey" CTA)
2. Registration Form
3. Email Verification Pending Screen
4. Email Verified Success Screen

**Key UI Elements:**
- **Landing Page Hero**: Compelling headline + "Start Your Journey" button
- **Registration Form**: Name, Email, Password fields with real-time validation
- **Password Strength Indicator**: Visual feedback on password strength
- **Check Email Screen**: Illustration + instructions + resend option
- **Success Screen**: Welcome message + auto-redirect to Create Club
