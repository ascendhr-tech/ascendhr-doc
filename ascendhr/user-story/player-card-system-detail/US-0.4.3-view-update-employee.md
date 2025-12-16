# View & Update Employee

**Story ID:** US-0.4.3  
**Epic:** 0.4 - Player Card System  
**Persona:** Scout (HR)

---

## User Story

> **As a** Scout (HR),  
> **I want to** view and update an employee's Player Card,  
> **So that** I can keep their profile and attributes current.

---

## Business Requirement/Logic

HR สามารถเข้าดูและแก้ไข Player Card ของพนักงานได้ทุกเมื่อ เมื่อมีการแก้ไข Attributes ระบบจะคำนวณ Current Ability ใหม่โดยอัตโนมัติ ทุกการเปลี่ยนแปลงจะถูกบันทึกเป็น Audit Log เพื่อติดตามประวัติ

**Key Business Rules:**
- ทุกการแก้ไขต้องมีการ validate ก่อน save
- เมื่อ Attributes เปลี่ยน, Current Ability จะถูก recalculate
- ทุกการเปลี่ยนแปลงถูกบันทึกใน Audit Log
- ปุ่ม Save จะ disable หากไม่มีการเปลี่ยนแปลง
- สามารถดูประวัติการเปลี่ยนแปลงได้ใน History tab

---

## Acceptance Criteria

### Scenario 1: Successfully View and Update Employee

**Given**
- Scout is logged in with `employee:update` permission
- Employee "John Doe" exists in the system

**When**
- Scout clicks on "John Doe" from the employee list
- Scout clicks "Edit" button
- Scout updates the department from "Engineering" to "Product"
- Scout adjusts "Leadership" attribute from 12 to 15
- Scout clicks "Save Changes"

**Then**
- System navigates to John's Player Card detail page
- System switches to edit mode when "Edit" clicked
- System validates changes in real-time
- System saves updates to database
- System recalculates Current Ability based on new attribute value
- System logs all changes to audit history
- System shows success notification "Changes saved"
- System returns to view mode

---

### Scenario 2: Invalid Input During Edit

**Given**
- Scout is in edit mode on an employee's Player Card

**When**
- Scout enters invalid email format "john@invalid"
- Scout tries to save

**Then**
- System shows field-level error "Please enter a valid email"
- System prevents save until error is corrected
- Invalid field is highlighted

---

### Scenario 3: No Changes Made

**Given**
- Scout is in edit mode on an employee's Player Card
- Scout has not made any changes

**When**
- Scout views the form without modifying anything

**Then**
- "Save Changes" button is disabled
- System indicates no pending changes

---

### Scenario 4: View Attribute Change History

**Given**
- Scout is viewing an employee's Player Card
- Employee has been updated multiple times

**When**
- Scout clicks on "History" tab

**Then**
- System displays timeline of all attribute changes
- Each entry shows: date, who changed, what changed (old → new value)
- Changes are sorted newest first

---

## UI/UX Notes

**Screens Involved:**
1. Player Card Detail (view mode)
2. Player Card Detail (edit mode)
3. Attribute Edit Panel (sliders)
4. Change History Tab (audit log)

**Key UI Elements:**
- **Player Card View**: Profile photo, basic info, radar chart, ability scores
- **Edit Button**: Switches card to edit mode
- **Editable Fields**: Name, email, department, position (with validation)
- **Attribute Sliders**: 10 sliders for 1-20 rating, with live radar chart update
- **Current Ability Display**: Read-only, auto-recalculates on attribute change
- **Save/Cancel Buttons**: Save disabled until changes detected
- **History Tab**: Timeline view with change entries
- **Success Notification**: Toast message on save
