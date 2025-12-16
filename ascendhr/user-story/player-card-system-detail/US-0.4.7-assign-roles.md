# Assign Roles

**Story ID:** US-0.4.7  
**Epic:** 0.4 - Player Card System  
**Persona:** Scout (HR)

---

## User Story

> **As a** Scout (HR),  
> **I want to** assign roles to an employee,  
> **So that** they have appropriate system permissions.

---

## Business Requirement/Logic

Role กำหนด permissions ที่พนักงานมีในระบบ พนักงานหนึ่งคนสามารถมีหลาย roles ได้ การเปลี่ยนแปลง role จะมีผลทันที

ตัวอย่าง Roles:
- **Employee**: สิทธิ์พื้นฐานดู own profile
- **Team Lead**: approve leave, view team members
- **Manager**: all Team Lead + access reports
- **Scout (HR)**: manage employees
- **Admin**: full access

**Key Business Rules:**
- พนักงานต้องมีอย่างน้อย 1 role
- HR ที่ไม่มีสิทธิ์สูงพอ จะไม่เห็น high-level roles
- ทุกการเปลี่ยนแปลง role ถูก log ใน audit
- Permissions มีผลทันทีหลังบันทึก

---

## Acceptance Criteria

### Scenario 1: Successfully Assign Role

**Given**
- Scout is logged in with `role:assign` permission
- Employee "John" has role "Employee"

**When**
- Scout edits John's profile
- Scout clicks on "Roles" multi-select field
- Scout selects additional role "Team Lead"
- Scout clicks "Save"

**Then**
- System assigns "Team Lead" role to John
- John now has both "Employee" and "Team Lead" roles
- System updates John's permissions immediately
- System logs role change to audit: "Added 'Team Lead' role"
- Success notification is shown

---

### Scenario 2: High-Level Role Hidden for Insufficient Permission

**Given**
- Scout is logged in but does NOT have `admin:assign` permission
- "Admin" role exists in the system

**When**
- Scout opens the role selector for any employee

**Then**
- "Admin" role is hidden or disabled in the dropdown
- Scout cannot assign Admin role
- Only assignable roles are shown/enabled

---

### Scenario 3: Remove Role from Employee

**Given**
- Employee "Jane" has roles: "Employee", "Team Lead", "Manager"

**When**
- Scout edits Jane's profile
- Scout deselects "Manager" role
- Scout clicks "Save"

**Then**
- System removes "Manager" role from Jane
- Jane now has only "Employee" and "Team Lead"
- System updates permissions (removes Manager permissions)
- System logs: "Removed 'Manager' role"

---

### Scenario 4: Cannot Remove Last Role

**Given**
- Employee "Mike" has only one role: "Employee"

**When**
- Scout tries to deselect the "Employee" role

**Then**
- System prevents removal
- Shows message "Employee must have at least one role"
- "Employee" role checkbox cannot be unchecked

---

## UI/UX Notes

**Screens Involved:**
1. Role Assignment Field (multi-select)
2. Role Selector Dropdown

**Key UI Elements:**
- **Roles Field**: Multi-select dropdown with checkboxes
- **Role Chips**: Show currently assigned roles as removable chips
- **Role Dropdown**: List of available roles with descriptions
- **Disabled Roles**: High-level roles shown but disabled if no permission
- **Tooltip**: Hover on disabled role shows "Insufficient permission"
- **Role Badges**: Display on Player Card showing assigned roles
- **Audit Log Entry**: Shows role changes in history tab
