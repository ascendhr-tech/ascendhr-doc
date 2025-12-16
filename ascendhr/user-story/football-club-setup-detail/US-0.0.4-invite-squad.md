# Invite Initial Squad (Scouts/Staff)

**Story ID:** US-0.0.4  
**Epic:** 0.0 - Football Club Setup  
**Persona:** Club Owner

---

## User Story

> **As a** Club Owner,  
> **I want to** invite my HR team and managers,  
> **So that** they can help me add the rest of the squad.

---

## Business Requirement/Logic

หลังจาก Owner สร้าง Player Card ของตัวเองเสร็จแล้ว จะสามารถเชิญทีมงานคนอื่น (เช่น HR, Managers) เข้ามาร่วมใช้งานระบบได้ คนที่ถูกเชิญจะได้รับ email invitation และต้องสร้าง Player Card ของตัวเองเช่นกัน

**Key Business Rules:**
- Invitation email มีอายุ 7 วัน
- สามารถเชิญหลายคนพร้อมกันได้ (comma-separated emails)
- ต้องกำหนด Role ให้ผู้ถูกเชิญ (Scout/HR, Manager, Employee)
- ผู้ถูกเชิญจะต้องสร้าง Player Card ของตัวเองหลังยอมรับ invitation
- สามารถข้าม (Skip) ขั้นตอนนี้ได้ และกลับมาเชิญทีหลัง

---

## Acceptance Criteria

### Scenario 1: Successfully Invite Team Members

**Given**
- Club Owner has created their club
- Club Owner has completed their player card

**When**
- Owner clicks "Invite Team Members"
- Owner enters email addresses (one or comma-separated)
- Owner selects role for invitees (Scout/HR, Manager, Employee)
- Owner adds optional personal message
- Owner clicks "Send Invitations"

**Then**
- System validates all email addresses
- System sends invitation emails to all valid addresses
- System shows "Invitations sent" summary with count
- Pending invitations are tracked in the system

---

### Scenario 2: Invitee Successfully Accepts Invitation

**Given**
- Invitee has received invitation email
- Invitation link is still valid (within 7 days)

**When**
- Invitee clicks the invitation link in email
- Invitee is taken to Accept Invitation page
- Invitee sets their password
- Invitee clicks "Join the Club"

**Then**
- System creates user account for invitee
- System assigns the role specified in invitation
- System redirects invitee to "Setup Your Player Card" flow
- Invitee must create their own Player Card (same as US-0.0.3)

---

### Scenario 3: Email Already in System

**Given**
- Club Owner is on the invite modal
- Email "existing@company.com" is already registered

**When**
- Owner enters "existing@company.com"
- Owner attempts to send invitation

**Then**
- System shows error "Already a member of this club" for that email
- Other valid emails can still be sent
- Form allows correction

---

### Scenario 4: Skip Invitations

**Given**
- Club Owner is on the invite modal
- Owner does not want to invite anyone now

**When**
- Owner clicks "Skip for now" or closes the modal

**Then**
- System allows owner to proceed without inviting
- Owner can invite team members later from settings
- System shows dashboard or next onboarding step

---

### Scenario 5: Invitation Link Expired

**Given**
- Invitee has received invitation email
- Invitation link is older than 7 days

**When**
- Invitee clicks the expired invitation link

**Then**
- System shows error "Invitation has expired"
- System suggests contacting Club Owner to resend
- Invitee cannot proceed with this link

---

## UI/UX Notes

**Screens Involved:**
1. Invite Team Modal (Owner's side)
2. Invitation Sent Confirmation (Owner's side)
3. Accept Invitation Page (Invitee's side)
4. Set Password Page (Invitee's side)

**Key UI Elements:**
- **Invite Modal**: Email input (supports multiple), role selector, message textarea
- **Email Input**: Auto-split by comma, validate each email, show chips
- **Role Selector**: Dropdown with Scout/HR, Manager, Team Lead, Employee
- **Pending Invitations List**: Shows sent invitations with status (pending/accepted)
- **Accept Page**: Welcome message, password creation form
- **Password Form**: Password + confirm password with strength indicator
- **Skip Link**: "Skip for now" option in modal footer
