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
HR creates a new employee profile with FM-style attributes during onboarding using a 3-step wizard.

### Preconditions
- Scout is logged in with `employee:create` permission
- Departments and Positions already exist with Zone assignments

### Main Flow (3-Step Wizard)

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Click "Add Player" button | Display Step 1: Basic Info form |
| 2 | Fill name, email, phone | Validate required fields in real-time |
| 3 | Click "Next: Assignment" | Navigate to Step 2 |
| 4 | Select Department | Show Zone badge (Attack/Midfield/Defense/Support) |
| 5 | Select Position | Filter positions by department, show cascading dropdown |
| 6 | Set "Reports To" manager | Show manager dropdown |
| 7 | Click "Next: Attributes" | Navigate to Step 3 |
| 8 | Rate 5 core attributes using 1-20 sliders | Show **spider chart with position requirements comparison** |
| 9 | View live Fit Score | Calculate fit % against position requirements |
| 10 | View Gap Analysis | Show Above/Meets/Below counts for each attribute |
| 11 | Click "Create Player" | Create employee record |
| 12 | - | Auto-create user account with zone color |
| 13 | - | Show success with Player Card preview |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 2a | Email already exists | Show error "Email already registered" |
| 4a | Department changed | Reset position dropdown, update zone display |
| 8a | Attribute below position requirement | Show warning icon on slider |

### Key Features
- **Zone-based Departments:** Each department has a zone color (Attack=Red, Midfield=Green, Defense=Blue, Support=Purple)
- **Position Comparison Spider Chart:** Dashed line shows position requirements, filled area shows input values
- **Live Fit Score:** Updates in real-time as sliders move
- **Gap Analysis Panel:** Shows how many attributes are Above/Meets/Below expectation

### Screens
1. Step 1: Basic Information (name, email, phone)
2. Step 2: Assignment (department with zone, position, manager)
3. Step 3: Attributes (sliders + spider chart + fit score panel)
4. Live Preview Card (reflects current values with zone styling)

**HTML Mockup:** [02-create-employee.html](file:///Users/gdrom/Desktop/allkons/ascend-hr-docs/ascendhr/design/player-card-system/02-create-employee.html)

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
| 1 | Navigate to "Players" page | Display stats row (total, Attack, Midfield, Defense, Support counts) |
| 2 | View player gallery | Show FIFA-style cards with zone-colored headers |
| 3 | Click Zone filter pill (All/Attack/Midfield/Defense/Support) | Filter cards by zone, update counts |
| 4 | Type in search box | Filter cards by name/position in real-time |
| 5 | Click "Sort by Rating" | Reorder cards by Overall rating |
| 6 | Hover on player card | Show action buttons (Select, Delete) |
| 7 | Click on player card | Navigate to Player Card detail |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 3a | No players in zone | Show "No players in this zone" |
| 4a | No search results | Show "No players match your search" |

### Key Features
- **Zone Stats Row:** Shows player count by zone with color-coded badges
- **Zone Filter Pills:** Quick filter by Attack/Midfield/Defense/Support
- **FIFA-style Cards:** Overall rating, position badge, zone-colored header
- **Hover Actions:** Select (for compare) and Delete buttons

### Screens
1. Player Gallery (Card Grid with zone-colored headers)
2. Stats Row (Total and zone counts)
3. Filter Bar (Zone pills, search, sort)
4. Compare Modal (side-by-side spider charts)

**HTML Mockup:** [04-player-gallery.html](file:///Users/gdrom/Desktop/allkons/ascend-hr-docs/ascendhr/design/player-card-system/04-player-gallery.html)

---

## US-0.4.3: View & Update Employee (Update Attributes Flow)

> **As a** Scout (HR),  
> **I want to** view and update an employee's Player Card attributes,  
> **So that** I can track their growth and maintain accurate skill profiles.

### Scenario
HR updates an employee's skills after a performance review using a guided wizard.

### Preconditions
- User is logged in with `employee:update` permission
- Employee exists with existing attributes

### Main Flow (Update Attributes - 3-Step Wizard)

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Click on player from gallery | Navigate to Player Card detail page |
| 2 | View Hero Section | Display **large spider chart** comparing actual vs position requirements |
| 3 | View Fit Score | Show 92% badge with gap analysis (Above/Meets/Below counts) |
| 4 | View Attribute Cards | Display 8 attributes in grid with value, required, and +/- indicators |
| 5 | Click **"📊 Update Attributes"** button | Open 3-step Update Wizard |
| 6 | **Step 1:** Select trigger type | Choose from: Performance Review, Training, Project, Observation, Peer Feedback |
| 7 | Click Continue | Navigate to Step 2 |
| 8 | **Step 2:** Adjust attribute sliders | Show current vs new value with ▲+X / ▼-X indicators |
| 9 | Add justification for each change | Enter text explaining why attribute changed |
| 10 | Click "Preview Impact" | Navigate to Step 3 |
| 11 | **Step 3:** Review before/after fit scores | Show 85% → 92% comparison |
| 12 | View changes summary | List all attribute changes with justifications |
| 13 | Add evidence link (optional) | Link to review document, certificate, etc. |
| 14 | Click "Confirm & Save" | Save changes to history |
| 15 | - | Update player card with new values |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 8a | No changes made | Show "No changes" in preview |
| 14a | Cancel clicked | Discard changes, return to detail page |

### Key Features
- **Hero Spider Chart:** Large chart showing position requirements (dashed) vs actual (filled)
- **Fit Score Display:** Prominent percentage with color coding (green=high, red=low)
- **Attribute Cards Grid:** 8 cards showing value, requirement, and gap indicator
- **Trigger Selection:** Captures WHY the update is happening (for analytics)
- **Justification Fields:** Free text explaining each change (for audit trail)
- **Impact Preview:** Before/After comparison of fit score

### Screens
1. Player Card Detail (hero spider chart, fit score, attribute cards)
2. Update Wizard Step 1: Trigger Selection
3. Update Wizard Step 2: Attribute Adjustment with Justification
4. Update Wizard Step 3: Impact Preview
5. Attribute History Timeline

**HTML Mockup:** [03-employee-detail.html](file:///Users/gdrom/Desktop/allkons/ascend-hr-docs/ascendhr/design/player-card-system/03-employee-detail.html)

---

## US-0.4.3b: Change Position/Department (Transfer Flow)

> **As a** Scout (HR),  
> **I want to** change an employee's position or department,  
> **So that** I can track promotions, demotions, lateral moves, and department transfers like player transfers in football.

### Scenario
HR promotes an employee or transfers them to a different department using a guided wizard with fit analysis.

### Preconditions
- User is logged in with `employee:update` permission
- Employee exists with current position and department

### Main Flow (Change Position - 4-Step Wizard)

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Click **"🔄 Change Position"** button | Open 4-step Position Change Wizard |
| 2 | **Step 1:** Select change type | Choose: ⬆️ Promotion, ↔️ Lateral Move, 🔄 Department Transfer, ⬇️ Demotion |
| 3 | Click Continue | Navigate to Step 2 |
| 4 | **Step 2:** Select new department | Show Zone badge change (Midfield → Attack) |
| 5 | Select new position | Cascading dropdown filtered by department |
| 6 | Select new reporting manager | Dropdown of eligible managers |
| 7 | Set effective date | Calendar picker |
| 8 | Click "Analyze Fit" | Navigate to Step 3 |
| 9 | **Step 3:** View Fit Score Comparison | Show Current Role (92%) vs New Role (72%) |
| 10 | View Attribute Gap Analysis | List gaps (⚠️ Communication: -2) and strengths (✅ Technical: +8) |
| 11 | View Development Recommendations | Show suggested training/coaching |
| 12 | Click Continue | Navigate to Step 4 |
| 13 | **Step 4:** Review confirmation summary | Show FROM → TO with zone color change |
| 14 | Enter reason for change | Text field for justification |
| 15 | Attach approval document (optional) | Link to document |
| 16 | Click "Confirm Change" | Save position change to history |
| 17 | - | Update employee's position and department |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 4a | Same department selected | Position dropdown shows same-department roles |
| 9a | Fit score very low (<50%) | Show warning about skill gaps |
| 14a | Cancel clicked | Discard changes, return to detail page |

### Key Features
- **Change Type Selection:** Captures promotion/lateral/transfer/demotion for analytics
- **Zone Color Change:** Visual indicator when department changes (e.g., Midfield Green → Attack Red)
- **Fit Score Comparison:** Like FM position familiarity - shows how suited the employee is for new role
- **Gap Analysis:** Lists attributes that need development for new role
- **Development Recommendations:** Suggests training based on gaps (like FM training suggestions)

### Data Model
```javascript
{
  type: "lateral_transfer",
  previousPosition: { department: "Engineering", position: "Tech Lead", zone: "midfield", fitScore: 92 },
  newPosition: { department: "Product", position: "Product Manager", zone: "attack", fitScore: 72 },
  effectiveDate: "2025-01-15",
  reason: "Career development interest",
  developmentPlan: ["Stakeholder management training", "Product roadmap workshop"]
}
```

### Screens
1. Position Change Wizard Step 1: Change Type Selection
2. Position Change Wizard Step 2: New Position Selection
3. Position Change Wizard Step 3: Fit Score Comparison & Gap Analysis
4. Position Change Wizard Step 4: Confirmation & Reason

**HTML Mockup:** [03-employee-detail.html](file:///Users/gdrom/Desktop/allkons/ascend-hr-docs/ascendhr/design/player-card-system/03-employee-detail.html)

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
