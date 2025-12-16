# Change Employment Status

**Story ID:** US-0.4.4  
**Epic:** 0.4 - Player Card System  
**Persona:** Scout (HR)

---

## User Story

> **As a** Scout (HR),  
> **I want to** change an employee's status,  
> **So that** I can reflect leaves, suspensions, or terminations.

---

## Business Requirement/Logic

HR สามารถเปลี่ยนสถานะพนักงานได้ ซึ่งแต่ละสถานะมีผลต่อการใช้งานระบบของพนักงานแตกต่างกัน:

| Status | Effect |
|--------|--------|
| Active | ใช้งานระบบได้ปกติ |
| On Leave | ยังคงมี access แต่ถูก flag ว่าลาพัก |
| Suspended | ถูก suspend access ชั่วคราว |
| Terminated | ปิด user account ถาวร |

**Key Business Rules:**
- ทุกการเปลี่ยนสถานะต้องระบุ effective date
- ต้องระบุเหตุผลในการเปลี่ยนสถานะ
- สถานะ Terminated ต้องกรอก handover notes
- เมื่อ Terminated, user account จะถูก deactivate
- ทุกการเปลี่ยนสถานะถูก log ไว้ใน history

---

## Acceptance Criteria

### Scenario 1: Successfully Change Status to On Leave

**Given**
- Scout is logged in with `employee:update` permission
- Employee "John Doe" has status "Active"

**When**
- Scout clicks "Change Status" from John's Player Card
- Scout selects "On Leave" from status dropdown
- Scout fills effective date and reason
- Scout clicks "Confirm"

**Then**
- System updates employee status to "On Leave"
- System logs status change to history
- System shows confirmation message
- Employee's Player Card shows new status badge

---

### Scenario 2: Terminate Employee with Extended Form

**Given**
- Scout is logged in with `employee:update` permission
- Employee "Jane Smith" has status "Active"

**When**
- Scout clicks "Change Status" from Jane's Player Card
- Scout selects "Terminated"

**Then**
- System displays extended termination form with:
  - Exit date (required)
  - Termination reason (required)
  - Handover notes (optional)
- Scout fills all required fields
- Scout clicks "Confirm"

**And Then**
- System updates employee status to "Terminated"
- System deactivates employee's user account
- System logs termination to history
- Employee can no longer log into the system

---

### Scenario 3: Missing Required Fields

**Given**
- Scout is on the Status Change modal
- Scout has selected a new status

**When**
- Scout leaves required fields empty (effective date, reason)
- Scout clicks "Confirm"

**Then**
- System shows validation errors on required fields
- Modal remains open for correction
- Status is not changed

---

### Scenario 4: View Status History

**Given**
- Scout is viewing an employee's Player Card
- Employee's status has been changed multiple times

**When**
- Scout views the Status History panel

**Then**
- System displays timeline of all status changes
- Each entry shows: date changed, from status → to status, changed by, reason

---

## UI/UX Notes

**Screens Involved:**
1. Status Change Modal
2. Termination Form (extended fields)
3. Status History Panel

**Key UI Elements:**
- **Change Status Button**: Available on Player Card quick actions
- **Status Dropdown**: Active, On Leave, Suspended, Terminated
- **Effective Date Picker**: Calendar picker, default today
- **Reason Field**: Text input (required)
- **Termination Form Extension**: Exit date, reason, handover notes
- **Confirm/Cancel Buttons**: Primary/secondary actions
- **Status Badge**: Color-coded on Player Card (green=Active, yellow=On Leave, red=Terminated)
- **Status History Timeline**: Chronological list of status changes
