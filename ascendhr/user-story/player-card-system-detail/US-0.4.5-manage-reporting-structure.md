# Manage Reporting Structure

**Story ID:** US-0.4.5  
**Epic:** 0.4 - Player Card System  
**Persona:** Scout (HR)

---

## User Story

> **As a** Scout (HR),  
> **I want to** set who an employee reports to,  
> **So that** the org hierarchy is correct for approvals.

---

## Business Requirement/Logic

การจัดโครงสร้างผู้บังคับบัญชาเป็นสิ่งสำคัญสำหรับระบบ approval เช่น การอนุมัติวันลา หรือการอนุมัติค่าใช้จ่าย

**Key Business Rules:**
- พนักงานไม่สามารถ report to ตัวเอง
- ห้ามสร้าง circular reference (เช่น A → B → A)
- Manager dropdown แสดงเฉพาะพนักงานที่มีสิทธิ์เป็น manager
- Direct reports จะแสดงบน Player Card ของ manager
- เมื่อเปลี่ยน org structure, approval workflows ที่เกี่ยวข้องจะถูก update

---

## Acceptance Criteria

### Scenario 1: Successfully Assign Manager

**Given**
- Scout is logged in with `employee:update` permission
- Employee "John Doe" exists without a manager
- Employee "Sarah Manager" exists and can be a manager

**When**
- Scout edits John's profile
- Scout clicks "Reports To" dropdown
- Scout searches and selects "Sarah Manager"
- Scout clicks "Save"

**Then**
- System updates John's reporting relationship to Sarah
- System validates no circular reference is created
- Sarah's Player Card now shows John in "Direct Reports" list
- System shows success notification

---

### Scenario 2: Cannot Report to Self

**Given**
- Scout is editing employee "John Doe"

**When**
- Scout opens "Reports To" dropdown
- Scout attempts to select "John Doe"

**Then**
- System shows error "Cannot report to self"
- Selection is rejected
- Dropdown remains open for another selection

---

### Scenario 3: Circular Reference Detected

**Given**
- "John" reports to "Sarah"
- "Sarah" currently has no manager

**When**
- Scout edits Sarah's profile
- Scout tries to set Sarah's manager as "John"
- Scout clicks "Save"

**Then**
- System shows error "Would create circular hierarchy"
- Change is rejected
- Original relationship remains unchanged

---

### Scenario 4: View Direct Reports

**Given**
- Manager "Sarah" has 3 direct reports: John, Jane, Mike

**When**
- Scout views Sarah's Player Card

**Then**
- System displays "Direct Reports" section
- Shows list of John, Jane, Mike with their quick info
- Each direct report is clickable to view their Player Card

---

## UI/UX Notes

**Screens Involved:**
1. Reports To Field (in employee form)
2. Manager Dropdown (searchable)
3. Direct Reports List (on manager's card)

**Key UI Elements:**
- **Reports To Dropdown**: Searchable, shows manager name + position
- **Search in Dropdown**: Type-ahead search for manager
- **Clear Button**: Option to remove current manager (make root)
- **Direct Reports Section**: List view on Manager's Player Card
- **Report Count Badge**: Shows "(3 direct reports)" on Manager
- **Org Tree Preview**: Optional mini visualization of hierarchy
