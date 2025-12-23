# Attribute Configuration System

**Story ID:** US-0.5.3  
**Epic:** 0.5: Formation View + Squad Builder  
**Persona:** Club Owner (Admin)

---

## User Story

> **As a** Club Owner,  
> **I want to** configure Core and Specialist attributes,  
> **So that** I can customize the rating system to my specific company culture and industry.

---

## Business Requirement/Logic

**Key Business Rules:**
- **Categories:**
  - **Core:** Apply to EVERY employee (e.g., Leadership, Teamwork).
  - **Specialist:** Linked to specific Zones (e.g., "Closing" for Attack/Sales, "Coding" for Midfield/Engineering).
- **Scale:** All attributes are rated on a 1-20 scale (Football Manager style).
- **Iconography:** Attributes should have icons/emojis for visual recognition.

---

## Acceptance Criteria

### Scenario 1: Add New Specialist Attribute

**Given**
- Owner wants to track "Rust Programming" skills

**When**
- Owner navigates to "Settings" > "Attributes"
- Owner clicks "Add Attribute"
- Owner enters Name "Rust", Code "rust_lang"
- Owner selects Category "Specialist" and Zone "Midfield" (Engineering)
- Owner saves

**Then**
- System adds "Rust" to the library of available attributes
- "Rust" becomes available to select when configuring Engineering roles
- "Rust" does NOT appear by default for Sales roles (Attack zone)

### Scenario 2: Edit Core Attribute

**Given**
- "Adaptability" is a Core attribute

**When**
- Owner changes the name from "Adaptability" to "Agility"
- Owner updates the description
- Owner saves

**Then**
- System updates the definition globally
- All Player Cards displaying this attribute now show the label "Agility"

### Scenario 3: Delete Attribute

**Given**
- "Rust" specialist attribute exists in the attribute library
- Some employees have been rated on this attribute

**When**
- Owner clicks the 🗑️ delete button on the "Rust" attribute card
- Delete confirmation modal appears with warning

**Then**
- Modal shows "Delete Rust?" with warning icon
- Warning message states: "Employees currently rated on this attribute will lose their scores"
- Owner can click "Cancel" to abort or "Delete Attribute" to confirm
- If confirmed:
  - System removes the attribute from the library
  - All employee ratings for "Rust" are cleared
  - Positions requiring "Rust" are updated (attribute removed from requirements)
  - Success notification: "Attribute 'Rust' has been deleted"

---

## UI/UX Notes

**Screens Involved:**
1. **Attribute Library**:
   - Two main sections: **Core Attributes** (Top) and **Specialist Attributes** (Bottom, grouped by Zone).
   - Each attribute card shows: Icon, Name, Category badge.
   - Hover reveals action buttons: 👁️ View, ✏️ Edit, 🗑️ Delete
2. **Attribute Editor**:
   - Form fields: Name, Code (auto-generated slug), Description, Icon picker.
   - Category Toggle (Core vs Specialist).
   - Zone Dropdown (Visible only if Specialist).
3. **Delete Confirmation Modal**:
   - Warning icon and red-themed header
   - Attribute name in message
   - Warning about employee score impact
   - Cancel and Delete buttons
