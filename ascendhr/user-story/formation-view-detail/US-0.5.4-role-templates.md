# Role Templates Library

**Story ID:** US-0.5.4  
**Epic:** 0.5: Formation View + Squad Builder  
**Persona:** Club Owner (Admin)

---

## User Story

> **As a** Club Owner,  
> **I want to** browse and use pre-built role templates,  
> **So that** I don't have to configure every position from scratch.

---

## Business Requirement/Logic

**Key Business Rules:**
- **System Templates:** Read-only templates provided by the platform (e.g., "Software Developer", "Account Manager"). Cannot be deleted.
- **Custom Templates:** Owners can create their own templates based on existing positions.
- **Application:** Applying a template copies its attribute requirements to a Position. It does NOT enforce a permanent link (the position can diverge later).

---

## Acceptance Criteria

### Scenario 1: Apply Template to New Position

**Given**
- Owner is viewing the "Role Templates" gallery
- "Product Manager" template exists with standard attributes (Communication, Leadership)

**When**
- Owner clicks on "Product Manager" card
- Owner selects "Create Position from Template"
- Owner enters Title "Senior PM" & selects Dept "Product" (Midfield)
- Owner saves

**Then**
- New "Senior PM" position is created
- It inherits all attributes and weights from the "Product Manager" template
- Owner is redirected to the created position detail

### Scenario 2: Create Custom Template

**Given**
- A "Senior Backend Engineer" position exists with perfectly tuned attribute settings

**When**
- Owner views the position details
- Owner clicks "Save as Template"
- Owner names it "Senior Backend Standard"

**Then**
- System saves a new custom Role Template
- This template appears in the "My Templates" section of the library
- It can be reused for future hires

---

## UI/UX Notes

**Screens Involved:**
1. **Role Template Gallery**:
   - Grid of cards.
   - Filters: "System" vs "My Templates", Filter by Zone.
   - Cards show: Role Name, Zone Color, Top 3 Attributes.
2. **Template Detail Modal**:
   - Full attribute list breakdown.
   - "Use this Template" primary action button.
