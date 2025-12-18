# Position/Role Management

**Story ID:** US-0.5.2  
**Epic:** 0.5: Formation View + Squad Builder  
**Persona:** Club Owner (Admin)

---

## User Story

> **As a** Club Owner,  
> **I want to** define positions and configure their required attributes,  
> **So that** the system knows exactly what skills are needed for each role.

---

## Business Requirement/Logic

**Key Business Rules:**
- **Context:** Every Position belongs to exactly one Department.
- **Attribute Requirements:** Positions can define specific attribute targets:
  - **Critical:** Must match closely (High weight in Fit Score)
  - **Important:** Should match (Medium weight)
  - **Nice-to-have:** Bonus points (Low weight)
- **Role Templates:** Applying a template (US-0.5.4) overwrites/pre-fills the attribute requirements.
- **Pitch Coordinates:** Positions have (X, Y) coordinates relative to their Zone (or absolute 0-100 on pitch).

---

## Acceptance Criteria

### Scenario 1: Create Position with Role Template

**Given**
- "Engineering" department exists
- "Backend Developer" role template exists

**When**
- Owner enters Title "Senior Backend Engineer"
- Owner selects Department "Engineering"
- Owner selects Role Template "Backend Developer"
- Owner clicks "Save"

**Then**
- System creates the position linked to Engineering
- System automatically applies attributes from "Backend Developer" template (e.g., Coding > 15, System Design > 13)
- Position appears in the Position List under Engineering

### Scenario 2: Manual Attribute Configuration

**Given**
- Owner is creating a bespoke "Chief Innovation Officer" position
- No suitable template exists

**When**
- Owner enters Title "Chief Innovation Officer"
- Owner manually adds "Innovation" attribute as "Critical" (Min: 18)
- Owner manually adds "Leadership" attribute as "Important" (Min: 15)
- Owner sets Pitch Location to the center of Midfield (X:50, Y:50)
- Owner saves

**Then**
- System saves the custom attribute requirements
- System saves the pitch coordinates
- Future Fit Scores will be calculated based on these specific targets

---

## UI/UX Notes

**Screens Involved:**
1. **Position List**: Grouped by Zone/Department (e.g., Attack > Sales > Account Exec).
2. **Position Configuration Modal**:
   - **Details Tab**: Title, Dept, Template Selector.
   - **Attributes Tab**: List of attributes with "Importance" dropdowns and "Min Value" sliders.
   - **Location Tab**: Visual mini-pitch to drag-and-drop the position marker.
