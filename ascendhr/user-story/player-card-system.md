# Player Card System - User Stories

**Epic:** 0.4 - Player Card System  
**Version:** 1.0  
**Created:** December 11, 2024  
**Purpose:** User stories for UX flow design

---

## User Personas

| Persona | Role | Key Actions |
|---------|------|-------------|
| **Manager** | CEO/Leadership | View cards, compare players, analyze squad |
| **Scout** | HR | Create cards, rate attributes, import employees |

---

## US-0.4.1: Create Employee + Player Card

> **As a** Scout (HR),  
> **I want to** create a new employee with a Player Card,  
> **So that** I can add them to the squad and track their skills.

### Scenario
HR creates a new employee profile with FM-style attributes during onboarding.

### Preconditions
- Scout is logged in with `employee:create` permission
- Departments and Positions already exist

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Click "Add Employee" button | Display employee creation form |
| 2 | Fill basic info (name, email, department, position) | Validate required fields in real-time |
| 3 | Upload profile photo (optional) | Preview photo, validate size/format |
| 4 | Set "Reports To" manager (optional) | Show manager dropdown |
| 5 | Rate 10 attributes using 1-20 sliders | Calculate Current Ability score |
| 6 | Set Potential Ability | Validate ≥ Current Ability |
| 7 | Click "Create Player" | Create employee record |
| 8 | - | Auto-create user account |
| 9 | - | Send invitation email |
| 10 | - | Show success message + link to Player Card |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 2a | Email already exists | Show error "Email already registered" |
| 3a | Photo > 5MB | Show error "Photo must be under 5MB" |
| 6a | Potential < Current | Show error "Potential must be ≥ Current Ability" |
| 7a | Validation fails | Highlight invalid fields, stay on form |

### Screens
1. Employee List (with "Add Employee" button)
2. Create Employee Form
3. Attribute Rating Panel (sliders + radar chart preview)
4. Success Confirmation (with Player Card preview)

---

## US-0.4.2: Player Gallery & Search

> **As a** Scout (HR),  
> **I want to** search and filter the player gallery,  
> **So that** I can visually browse the squad and find specific players.

### Scenario
HR needs to find an employee to update their profile or compare attributes.

### Preconditions
- User is logged in with `employee:read` permission
- Employees exist in system

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Navigate to "Players" page | Display player gallery (FC-style Card Grid) |
| 2 | Type in search box | Filter cards by name/position in real-time |
| 3 | Apply filters (department, status) | Update grid with filtered results |
| 4 | Click "Sort by Rating" | Reorder cards by Current Ability |
| 5 | Click on player card | Navigate to Player Card detail |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 2a | No results found | Show "No players match your search" |
| 5a | Click "Import" or "Add Player" | Navigate to respective pages |

### Screens
1. Player Gallery (Card Grid with search, filters)
2. Filter Bar (Department, Status, Sort)

---

## US-0.4.3: View & Update Employee

> **As a** Scout (HR),  
> **I want to** view and update an employee's Player Card,  
> **So that** I can keep their profile and attributes current.

### Scenario
HR updates an employee's skills after a performance review.

### Preconditions
- User is logged in with `employee:update` permission
- Employee exists

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Click on employee from list | Navigate to Player Card detail page |
| 2 | View Player Card (photo, info, radar chart) | Display full profile |
| 3 | Click "Edit" button | Switch to edit mode |
| 4 | Update fields or attributes | Validate changes in real-time |
| 5 | Click "Save Changes" | Save updates with audit log |
| 6 | - | Recalculate Current Ability if attributes changed |
| 7 | - | Show success notification |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 4a | Invalid input | Show field-level error |
| 5a | No changes made | "Save" button disabled |

### Screens
1. Player Card Detail (view mode)
2. Player Card Detail (edit mode)
3. Attribute Edit Panel (sliders)
4. Change History Tab (audit log)

---

## US-0.4.4: Change Employment Status

> **As a** Scout (HR),  
> **I want to** change an employee's status,  
> **So that** I can reflect leaves, suspensions, or terminations.

### Scenario
HR needs to terminate an employee who is leaving the company.

### Preconditions
- User is logged in with `employee:update` permission
- Employee status is "Active"

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Click "Change Status" from employee card | Open status change modal |
| 2 | Select new status (On Leave, Suspended, Terminated) | Show additional fields based on status |
| 3 | Fill required fields (effective date, reason) | Validate inputs |
| 4 | Click "Confirm" | Update employee status |
| 5 | - | Log status change to history |
| 6 | - | If terminated: deactivate user account |
| 7 | - | Show confirmation message |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 2a | Select "Terminated" | Show termination form (exit date, reason, handover notes) |
| 4a | Missing required fields | Show validation errors |

### Screens
1. Status Change Modal
2. Termination Form (extended fields)
3. Status History Panel

---

## US-0.4.5: Manage Reporting Structure

> **As a** Scout (HR),  
> **I want to** set who an employee reports to,  
> **So that** the org hierarchy is correct for approvals.

### Scenario
HR assigns a new employee to report to their team manager.

### Preconditions
- User is logged in with `employee:update` permission
- Managers exist in system

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Edit employee profile | Show "Reports To" field |
| 2 | Click manager dropdown | Display searchable list of managers |
| 3 | Select manager | Set reporting relationship |
| 4 | Click "Save" | Update hierarchy |
| 5 | - | Validate no circular reference |
| 6 | - | Show updated org info |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 3a | Select self | Show error "Cannot report to self" |
| 5a | Circular reference detected | Show error "Would create circular hierarchy" |

### Screens
1. Reports To Field (in employee form)
2. Manager Dropdown (searchable)
3. Direct Reports List (on manager's card)

---

## US-0.4.6: Bulk Import Employees

> **As a** Scout (HR),  
> **I want to** import multiple employees via CSV,  
> **So that** I can quickly onboard the entire team.

### Scenario
HR uploads a spreadsheet of 50 new employees during company onboarding.

### Preconditions
- User is logged in with `employee:import` permission

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Click "Import Employees" | Open import wizard |
| 2 | Click "Download Template" | Download CSV template file |
| 3 | Fill template with employee data | (offline action) |
| 4 | Drag-drop or select CSV file | Upload and parse file |
| 5 | - | Validate each row |
| 6 | - | Show preview: valid rows (green), invalid rows (red) |
| 7 | Review validation results | Click row to see error details |
| 8 | Click "Import Valid Rows" | Create employee records |
| 9 | - | Send invitation emails |
| 10 | - | Show summary: X created, Y skipped, Z errors |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 4a | Wrong file format | Show error "Please upload CSV file" |
| 6a | All rows invalid | Disable import button, show errors |
| 6b | Some rows invalid | Allow import of valid rows only |

### Screens
1. Import Wizard (step indicator)
2. Template Download Section
3. File Upload Zone (drag-drop)
4. Validation Preview Table (valid/invalid highlighting)
5. Error Detail Panel
6. Import Summary (success/skip/error counts)

---

## US-0.4.7: Assign Roles

> **As a** Scout (HR),  
> **I want to** assign roles to an employee,  
> **So that** they have appropriate system permissions.

### Scenario
HR assigns "Team Lead" role to a promoted employee.

### Preconditions
- User is logged in with `role:assign` permission
- Roles are configured in system

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Edit employee profile | Show "Roles" field |
| 2 | Click role multi-select | Display available roles |
| 3 | Select/deselect roles | Update selection |
| 4 | Click "Save" | Assign roles to user |
| 5 | - | Update user permissions |
| 6 | - | Log role change to audit |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 2a | No permission to assign high-level role | Role is disabled/hidden |

### Screens
1. Role Assignment Field (multi-select)
2. Role Selector Dropdown

---

## US-0.4.8a: View Player Card

> **As a** Manager (CEO),  
> **I want to** view an employee's Player Card,  
> **So that** I can assess their skills at a glance.

### Scenario
CEO reviews a potential promotion candidate's abilities.

### Preconditions
- User is logged in with `employee:read` permission
- Employee has attributes rated

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Navigate to Player Gallery or search | Display employee cards |
| 2 | Click on Player Card | Open full Player Card view |
| 3 | View radar chart | See all 10 attributes visualized |
| 4 | View ability scores | See Current vs Potential |
| 5 | Click "History" tab | View attribute changes over time |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 2a | Employee has no attributes | Show "Not yet rated" message |

### Screens
1. Player Gallery (card grid)
2. Player Card Full View
3. Radar Chart Component
4. Attribute History Timeline

---

## US-0.4.8b: Compare Players

> **As a** Manager (CEO),  
> **I want to** compare two or more Player Cards side-by-side,  
> **So that** I can make informed decisions about promotions or team composition.

### Scenario
CEO compares two candidates for a senior position.

### Preconditions
- User is logged in with `employee:read` permission
- At least 2 employees exist

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | From gallery, select first player | Add to comparison (show badge) |
| 2 | Select additional players (up to 4) | Add to comparison list |
| 3 | Click "Compare Selected" | Open comparison modal |
| 4 | View side-by-side cards | Display all selected players |
| 5 | View attribute comparison | Show differences (green=higher, red=lower) |
| 6 | Click "Export" (optional) | Download comparison as image/PDF |
| 7 | Click "Close" | Return to gallery |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 1a | Only 1 player selected | "Compare" button disabled |
| 2a | Try to add 5th player | Show message "Maximum 4 players" |

### Screens
1. Player Gallery (with selection checkboxes)
2. Comparison Bar (shows selected count)
3. Comparison Modal (side-by-side view)
4. Attribute Difference Highlights
5. Export Options Panel

---

## Quality Checklist

- [x] All user stories from Epic 0.4 are included (8 stories + 2 sub-stories)
- [x] Each story has `As a... I want to... So that...` statement
- [x] Each story has Main Flow table (Step | User Action | System Response)
- [x] Each story has Alternative Flows for error cases
- [x] Each story lists Screens involved
- [x] Flows are detailed enough for Mermaid.js conversion

---

## Output Chain

```
This PRD → UX Agent (ascendhr-ux.md)
         → Creates Mermaid.js flow diagrams
         → Feeds into v0.dev for UI generation
```
