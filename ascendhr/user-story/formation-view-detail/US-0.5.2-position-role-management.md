# Position/Role Management

**Story ID:** US-0.5.2  
**Epic:** 0.5: Formation View + Squad Builder  
**Persona:** Club Owner (Admin)

---

## User Story

> **As a** Club Owner,  
> **I want to** define positions with full CRUD operations and configure their required attributes using an intuitive categorized interface,  
> **So that** the system knows exactly what skills are needed for each role and I can manage many attributes efficiently.

---

## Business Requirement/Logic

**Key Business Rules:**
- **Department Context:** Every Position belongs to exactly one Department.
- **Zone Inheritance:** Position zone is determined by its parent Department (not set directly on position).
- **Attribute Requirements:** Positions define specific attribute targets:
  - **Critical (★★★):** Must match closely (High weight in Fit Score)
  - **Important (★★):** Should match (Medium weight)
  - **Nice-to-have (★):** Bonus points (Low weight)
- **Scalable Attributes:** Attribute configuration supports many attributes via category organization and search.
- **Position Metrics:** Track employee count per position.

---

## Acceptance Criteria

### Scenario 1: Successfully Create Position

**Given**
- Club Owner is logged in with admin permissions
- "Engineering" department exists (in Midfield zone)

**When**
- Owner clicks "+ Add Position"
- Owner enters Title "Senior Backend Developer"
- Owner selects Department "Engineering"
- System automatically shows zone badge "⚙️ Midfield"
- Owner adds description
- Owner goes to Attributes tab and configures requirements
- Owner clicks "Save Position"

**Then**
- System creates the position linked to Engineering
- Position inherits "Midfield" zone from Engineering department
- Position appears in the Position List under Engineering accordion
- System shows a success message

---

### Scenario 2: Configure Attributes with Category Accordions

**Given**
- Owner is on the Attributes tab in Add/Edit Position modal
- Multiple attribute categories exist (Core, Technical, Business)

**When**
- Owner views the Attributes tab

**Then**
- Selected attributes appear as chips at the top with count
- Search box allows filtering attributes by name
- Attributes are grouped in collapsible category accordions
- Each attribute row shows: checkbox, icon, name, priority dropdown, min value input
- Selected attributes are highlighted with background color

**And When**
- Owner checks/unchecks attribute checkboxes
- Owner clicks X on a selected attribute chip

**Then**
- Attribute selection updates in real-time
- Selected count updates automatically
- Corresponding checkbox toggles in the list

---

### Scenario 3: View Position Details

**Given**
- Position "Frontend Developer" exists in Engineering
- Owner is on the Position Management page

**When**
- Owner clicks the View (👁️) icon on a position card

**Then**
- System opens Position Details modal
- Modal displays Overview (Title, Department with zone badge, Description)
- Modal displays Attribute Requirements table
- Modal displays Team Information (Current employees only)
- Modal displays Metadata (Created date, Last updated)
- Owner can click "Edit Position" or "Close"

---

### Scenario 4: Edit Position

**Given**
- An existing "UX/UI Designer" position
- Owner is on the Position Management page

**When**
- Owner clicks Edit (✏️) on the position
- Owner modifies the title, department, or attributes
- Owner clicks "Update Position"

**Then**
- System updates the position record
- Zone updates automatically if department changed
- Position appears in correct department accordion
- System shows success message

---

### Scenario 5: Delete Position with Confirmation

**Given**
- Position "Junior Developer" exists with 3 employees
- Owner is on the Position Management page

**When**
- Owner clicks the Delete (🗑️) icon on the position

**Then**
- System displays delete confirmation modal
- Modal shows warning: "This action cannot be undone"
- Modal displays position name highlighted
- Modal shows impact: "3 employees currently hold this position"
- Owner can click "Cancel" or "Delete Position"

---

### Scenario 6: Search and Filter Attributes

**Given**
- Owner is on the Attributes tab
- Many attributes exist across categories

**When**
- Owner types "leadership" in the search box

**Then**
- Only attributes matching the search term are displayed
- Non-matching attributes are hidden
- Categories with no matching attributes collapse

---

## UI/UX Notes

**Screens Involved:**
1. **Position Management Page** ([02-position-management.html](file:///Users/gdrom/Desktop/allkons/ascend-hr-docs/ascendhr/design/formation-view/02-position-management.html))
   - Stats cards row (3 cards: Total Positions, Total Employees, By Zone)
   - Department accordion sections
   - Position cards with hover actions

2. **Add/Edit Position Modal** (2 tabs):
   - **Details Tab:**
     - Position Title (required)
     - Department dropdown with auto zone badge (required)
     - Description
   - **Attributes Tab (Improved UX):**
     - Selected Attributes chips at top with count and remove buttons
     - Search input for filtering
     - Category accordions (Core, Technical, Business, etc.)
     - Each attribute: checkbox + icon + name + priority dropdown + min value input
     - Legend for priority levels

3. **Position Detail Modal**:
   - Overview section: Title, Department + Zone, Description
   - Attribute Requirements table
   - Team Information: Employees (no vacancies)
   - Metadata: Created, Updated
   - Actions: Edit, Close

4. **Delete Confirmation Modal**:
   - Warning alert (red)
   - Position name highlighted
   - Impact statement (employee count)
   - Actions: Cancel, Delete Position

**Key UI Elements:**
- **Selected Attribute Chips:** Removable chips showing selected attributes with priority and min value
- **Attribute Search:** Filter bar to find specific attributes
- **Category Accordions:** Collapsible sections for organizing many attributes
- **Attribute Row:** Inline checkbox + priority dropdown + min value input
- **Zone Badge:** Auto-appears when department selected

---

## Data Model

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| id | UUID | Yes | Unique identifier |
| title | String | Yes | Position title |
| department_id | UUID | Yes | Reference to department (zone inherited) |
| description | String | No | Position description |
| attributes | JSON | No | Array of {attr_id, priority, min_value} |
| created_at | DateTime | Yes | Creation timestamp |
| updated_at | DateTime | Yes | Last update timestamp |
