# Squad Builder

**Story ID:** US-0.5.6  
**Epic:** 0.5: Formation View + Squad Builder  
**Persona:** Team Manager

---

## User Story

> **As a** Team Manager,  
> **I want to** build specific squads using templates and drag-and-drop players,  
> **So that** I can form effective cross-functional teams with high fit scores.

---

## Business Requirement/Logic

**Key Business Rules:**
- **Squad vs. Dept:** A "Squad" is a cross-functional team (e.g., "Tiger Team") drawing members from different departments (Dev, Design, QA).
- **Squad Templates:** Squads are instances of a Squad Template (e.g., "Scrum Team").
- **Slots:** Templates define "Slots" (e.g., "Developer - 2 slots").
- **Fit Score Calculation:**
  - Formula: (Sum of (Employee Attribute Value × Requirement Weight)) / Max Possible Score.
  - Displayed as a percentage (e.g., 92% Fit).
- **Recommendations:** System should suggest the highest Fit Score employees for a selected slot.

---

## Acceptance Criteria

### Scenario 1: Create Squad from Scrum Template

**Given**
- "Scrum Team" template exists (requires 1 PM, 1 Designer, 3 Devs)
- Manager is on "Squads" page

**When**
- Manager clicks "Create Squad"
- Manager selects "Scrum Team" template
- Manager names it "Phoenix Project"

**Then**
- System creates a new squad container
- System generates the empty slots as per template (1 PM slot, 1 Designer slot, 3 Dev slots)
- Manager is taken to the Squad Builder Canvas for "Phoenix Project"

### Scenario 2: Assign Player with High Fit

**Given**
- Manager is building "Phoenix Project" squad
- "Frontend Developer" slot is empty

**When**
- Manager clicks the empty "Frontend Developer" slot
- System drawer opens showing "Recommended Players"
- "Alice" is at the top with a 95% Match
- Manager selects Alice

**Then**
- Alice is assigned to the slot
- The slot shows Alice's face
- The Fit Score (95%) is displayed on the card
- The Squad's overall "Team Average" stats update

### Scenario 3: Manual Search (No Fit Found)

**Given**
- Manager needs a "Rust Developer" but no one matches well (Top match is 40%)

**When**
- Manager clicks the Search bar in the player drawer
- Manager types "Bob" (a junior dev)
- Manager drags Bob into the slot

**Then**
- System assigns Bob
- System displays a "Low Fit" warning (e.g., Orange/Red score color) indicating a potential skill gap

---

## UI/UX Notes

**Screens Involved:**
1. **Squad Dashboard**: Card grid of active squads showing health (e.g., "5/6 Members").
2. **Squad Builder Canvas**:
   - Visual representation of the squad (e.g., 4-3-3 style layout or list).
   - **Empty Slots**: Dashed borders, "Add +".
   - **Filled Slots**: Player Card mini-view.
3. **Player Selection Drawer**:
   - Slide-out from right.
   - Tabs: "Recommended" (Algorithm), "Search" (Manual).
   - List items show: Name, Role, **Fit Score %**.
