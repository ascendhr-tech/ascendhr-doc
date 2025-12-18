# Department Management

**Story ID:** US-0.5.1  
**Epic:** 0.5: Formation View + Squad Builder  
**Persona:** Club Owner (Admin)

---

## User Story

> **As a** Club Owner,  
> **I want to** create departments and assign them to pitch zones (Attack, Midfield, Defense),  
> **So that** I can organize my company structure locally on the formation pitch.

---

## Business Requirement/Logic

**Key Business Rules:**
- **Zone Mapping:** Each department MUST be assigned to one of four zones:
  - **Attack:** Sales, Marketing, Business Development (Revenue Generators)
  - **Midfield:** Product, Engineering, Design, R&D (Value Creators)
  - **Defense:** Operations, Finance, Legal (Risk Managers & Enablers)
  - **Support:** HR, Admin, IT Support (Sidelines/Goalkeeper equivalent)
- **Visual Coding:** Zones determine the color coding on the pitch view (e.g., Red=Attack, Green=Midfield).
- **Unique Names:** Department names must be unique within the company.

---

## Acceptance Criteria

### Scenario 1: Successfully Create Department

**Given**
- Club Owner is logged in with admin permissions
- No department strictly named "Engineering" exists yet

**When**
- Owner navigates to "Formation Setup" > "Departments"
- Owner clicks "Add Department"
- Owner enters Name "Engineering"
- Owner selects Zone "Midfield"
- Owner clicks "Save"

**Then**
- System creates the "Engineering" department record
- System assigns the "Midfield" zone metadata
- System displays the new department in the list with a "Midfield" badge
- System shows a success toast message

### Scenario 2: Edit Department Zone

**Given**
- An existing "Product" department is currently in "Support" zone
- Owner is on the Department list

**When**
- Owner clicks "Edit" on "Product" department
- Owner changes Zone from "Support" to "Midfield"
- Owner clicks "Save"

**Then**
- System updates the department's zone
- The badge color changes to reflect the new "Midfield" zone
- Any visualizations (Pitch View) update to show Product in the Midfield area

---

## UI/UX Notes

**Screens Involved:**
1. **Department List Page**: Table view with Name, Zone badge, Employee Count, Actions.
2. **Add/Edit Department Modal**:
   - Name Input
   - Zone Selector (Radio cards with icons: ⚔️ Attack, ⚙️ Midfield, 🛡️ Defense, 🏥 Support)
   - Mini-pitch preview highlighting the selected zone area.
