# Employee List & Search

**Story ID:** US-0.4.2  
**Epic:** 0.4 - Player Card System  
**Persona:** Scout (HR)

---

## User Story

> **As a** Scout (HR),  
> **I want to** search and filter employees,  
> **So that** I can quickly find specific players in the squad.

---

## Business Requirement/Logic

ระบบต้องแสดงรายชื่อพนักงานทั้งหมดในรูปแบบ DataGrid พร้อมฟังก์ชันค้นหาและกรองข้อมูล เพื่อให้ HR สามารถหาพนักงานที่ต้องการได้อย่างรวดเร็ว

**Key Business Rules:**
- การค้นหาทำงานแบบ real-time (filter as you type)
- สามารถค้นหาได้ด้วย name, email, หรือ employee ID
- สามารถกรองตาม department, status, role, ability range
- Pagination รองรับ 20/50/100 รายการต่อหน้า
- คลิกที่แถวพนักงานจะเปิด Player Card detail

---

## Acceptance Criteria

### Scenario 1: Successfully View and Search Employee List

**Given**
- User is logged in with `employee:read` permission
- There are 100 employees in the system

**When**
- User navigates to "Squad" page
- User types "John" in the search box

**Then**
- System displays employee list in DataGrid format
- System filters list in real-time to show only employees matching "John" (by name, email, or ID)
- Matching results are highlighted
- Pagination adjusts to filtered results

---

### Scenario 2: Filter by Multiple Criteria

**Given**
- User is on the Employee List page
- Employees exist across multiple departments and statuses

**When**
- User applies filters:
  - Department: "Engineering"
  - Status: "Active"
  - Role: "Developer"

**Then**
- System updates list to show only employees matching ALL filter criteria
- Filter chips are displayed showing active filters
- User can remove individual filters to update results

---

### Scenario 3: Sort by Column

**Given**
- User is on the Employee List page with multiple employees displayed

**When**
- User clicks on "Name" column header

**Then**
- System reorders list alphabetically by name (ascending)
- User clicks again to toggle to descending order
- Sort indicator arrow is shown on the sorted column

---

### Scenario 4: Change Page Size and Navigate

**Given**
- User is on the Employee List page with 100 employees
- Default page size is 20

**When**
- User changes page size to 50
- User clicks "Next" page button

**Then**
- System updates display to show 50 employees per page
- System navigates to next page showing employees 51-100
- Pagination info updates accordingly

---

### Scenario 5: No Results Found

**Given**
- User is on the Employee List page

**When**
- User types "XYZ123NonExistent" in the search box

**Then**
- System shows message "No players match your search"
- Empty state illustration is displayed
- Clear search option is available

---

### Scenario 6: Quick Actions Menu

**Given**
- User is on the Employee List page
- User has appropriate permissions

**When**
- User clicks the quick action menu (⋮) on an employee row

**Then**
- System displays dropdown menu with options:
  - View Player Card
  - Edit Employee
  - Change Status
- Clicking an option navigates to the corresponding action

---

## UI/UX Notes

**Screens Involved:**
1. Employee List (DataGrid with search, filters, pagination)
2. Filter Panel (department, status, role, ability range)
3. Quick Actions Menu (dropdown)

**Key UI Elements:**
- **Search Box**: Full-text search with icon, placeholder "Search by name, email, ID..."
- **Filter Panel**: Collapsible sidebar or dropdown with checkboxes
- **DataGrid**: Columns for Name, Email, Department, Position, Status, Current Ability
- **Column Headers**: Clickable for sorting with direction indicator
- **Page Size Selector**: Dropdown (20/50/100)
- **Pagination**: Page numbers, prev/next buttons, total count
- **Quick Action Button**: ⋮ icon on each row, expands to menu
- **Empty State**: Illustration + "No players match your search" message
