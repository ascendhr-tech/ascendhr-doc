# Department Management

**Story ID:** US-0.5.1  
**Epic:** 0.5: Formation View + Squad Builder  
**Persona:** Club Owner (Admin)

---

## User Story

> **As a** Club Owner,  
> **I want to** manage departments with full CRUD operations and visualize them as an org chart by zone,  
> **So that** I can organize my company structure visually on the formation pitch with complete control over department data.

---

## Business Requirement/Logic

**Key Business Rules:**
- **Zone Mapping:** Each department MUST be assigned to one of four zones:
  - **Attack (Red):** Sales, Marketing, Business Development (Revenue Generators)
  - **Midfield (Green):** Product, Engineering, Design, R&D (Value Creators)
  - **Defense (Blue):** Operations, Finance, Legal (Risk Managers & Enablers)
  - **Support (Purple):** HR, Admin, IT Support (Sidelines/Goalkeeper equivalent)
- **Visual Coding:** Zones determine the color coding on both the org chart and pitch view.
- **Unique Names:** Department names must be unique within the company.
- **Department Head:** Each department can optionally have a department head assigned.
- **Metadata Tracking:** System tracks created date and last updated date for each department.
- **Cascade Delete:** Deleting a department removes all associated positions and employee assignments.

---

## Acceptance Criteria

### Scenario 1: Successfully Create Department

**Given**
- Club Owner is logged in with admin permissions
- No department with the same name exists yet

**When**
- Owner navigates to "Formation Setup" > "Departments"
- Owner clicks "+ Add Department"
- Owner enters Name (e.g., "Engineering")
- Owner enters Description (e.g., "Core product development")
- Owner selects Department Head from dropdown (optional)
- Owner selects Zone "Midfield" using visual zone selector
- Owner clicks "Save Department"

**Then**
- System creates the department record with all metadata
- System assigns the selected zone with correct color coding
- Department appears in both org chart and table view
- Department card shows in Midfield column of org chart
- Table row shows zone badge, department head, and employee count
- System shows a success toast message

---

### Scenario 2: View Department Details

**Given**
- Departments exist in the system
- Owner is on the Department Management page

**When**
- Owner clicks the view icon (👁️) on a department row
- OR Owner clicks on a department card in the org chart

**Then**
- System opens Department Details modal
- Modal displays Overview section (Name, Description, Zone badge)
- Modal displays Team Information (Department Head, Total Employees, Total Positions)
- Modal displays Metadata (Created On, Last Updated)
- Owner can click "Edit Department" to transition to edit mode
- Owner can click "Close" to dismiss the modal

---

### Scenario 3: Edit Department Zone

**Given**
- An existing "Product" department is currently in "Support" zone
- Owner is on the Department list

**When**
- Owner clicks "Edit" (✏️) on "Product" department
- OR Owner clicks "Edit Department" from the detail modal
- Owner changes Zone from "Support" to "Midfield"
- Owner updates Department Head
- Owner clicks "Update Department"

**Then**
- System updates the department's zone and head
- The badge color changes to reflect the new "Midfield" zone
- Org chart moves the department to the Midfield column
- Any visualizations (Pitch View) update to show Product in the Midfield area
- System shows a success toast message

---

### Scenario 4: Delete Department with Confirmation

**Given**
- A "Marketing" department exists with 8 employees and 4 positions
- Owner is on the Department Management page

**When**
- Owner clicks the delete icon (🗑️) on "Marketing" department
- System displays delete confirmation modal with warning

**Then**
- Modal shows warning: "This action cannot be undone"
- Modal displays department name "Marketing" highlighted
- Modal explains impact: "This will remove all positions and employee assignments"
- Owner can click "Cancel" to abort deletion
- Owner can click "Delete Department" (red button) to confirm

**And When**
- Owner confirms deletion by clicking "Delete Department"

**Then**
- System permanently deletes the department
- System removes all associated positions
- System removes all employee assignments
- Department disappears from org chart and table
- System shows a success toast message

---

### Scenario 5: View Organization Chart by Zones

**Given**
- Multiple departments exist across different zones
- Owner navigates to Department Management page

**When**
- Page loads completely

**Then**
- Org chart displays 4 zone columns (Attack, Midfield, Defense, Support)
- Each zone column shows correct color theme and icon:
  - Attack: Red with ⚔️
  - Midfield: Green with ⚙️
  - Defense: Blue with 🛡️
  - Support: Purple with 🏥
- Each zone shows department count header
- Department cards display:
  - Department name
  - Description (truncated)
  - Employee count badge (color-coded by zone)
  - Position count
- Cards are clickable and open detail modal
- Cards have hover effects (elevation, border color)

---

### Scenario 6: Duplicate Department Name Error

**Given**
- A department named "Engineering" already exists
- Owner is creating a new department

**When**
- Owner enters "Engineering" as department name
- Owner clicks "Save Department"

**Then**
- System shows error: "Department name already exists"
- Form remains open for correction
- Owner can modify the name and retry

---

### Scenario 7: Delete Prevention for Department with Active Employees

**Given**
- Department "Sales" has 12 active employees
- Owner attempts to delete "Sales" department

**When**
- Owner clicks delete and confirms

**Then**
- System shows warning about cascade deletion
- If business rules prevent deletion: System shows error "Cannot delete department with active employees"
- Owner must reassign employees before deletion
- (Or) System proceeds with cascade if business rules allow

---

## UI/UX Notes

**Screens Involved:**
1. **Department Management Page** ([01-department-management.html](file:///Users/gdrom/Desktop/allkons/ascend-hr-docs/ascendhr/design/formation-view/01-department-management.html))
   - Org Chart Section: 4-column layout by zones
   - Department Table: Full list with actions
   - Header with "+ Add Department" button

2. **Add/Edit Department Modal**:
   - Department Name input (required)
   - Description textarea
   - Department Head dropdown selector
   - Zone Selector (4 radio cards with icons: ⚔️ Attack, ⚙️ Midfield, 🛡️ Defense, 🏥 Support)
   - Visual feedback on zone selection

3. **Department Detail Modal**:
   - Overview section: Name, Description, Zone badge
   - Team Information section: Head, Employees, Positions
   - Metadata section: Created date, Updated date
   - Actions: "Edit Department", "Close"

4. **Delete Confirmation Modal**:
   - Warning alert (red background)
   - Department name highlighted
   - Impact description
   - Actions: "Cancel", "Delete Department" (destructive red)

**Key UI Elements:**
- **Org Chart Cards**: Interactive cards with hover elevation effect, zone-colored employee count badge
- **Zone Selector**: 4 clickable cards with icons, selected state shows zone color background
- **Action Icons**: View (👁️), Edit (✏️), Delete (🗑️) with hover states
- **Zone Badges**: Pill-shaped badges with zone-specific colors and icons
- **Table**: Sortable columns with Name, Zone, Department Head, Positions, Employees, Created date, Actions

---

## Data Model

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| id | UUID | Yes | Unique identifier |
| name | String | Yes | Department name (unique per company) |
| description | String | No | Brief description |
| zone | Enum | Yes | attack, midfield, defense, support |
| department_head_id | UUID | No | Reference to user |
| created_at | DateTime | Yes | Creation timestamp |
| updated_at | DateTime | Yes | Last update timestamp |
| company_id | UUID | Yes | Reference to company |
