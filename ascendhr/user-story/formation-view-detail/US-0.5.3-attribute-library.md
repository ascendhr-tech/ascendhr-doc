# Attribute Library

**Story ID:** US-0.5.3  
**Epic:** 0.5: Formation View + Squad Builder  
**Persona:** Club Owner (Admin)

---

## User Story

> **As a** Club Owner,  
> **I want to** define attributes with clear scoring criteria (1-20 scale) and data sources,  
> **So that** I have consistent, quality data for HR analytics and future prediction engines.

---

## Business Requirement/Logic

**Key Business Rules:**
- **Category Organization:** Attributes are grouped into categories (Core/Soft Skills, Technical, Business, Creative)
- **Scale Definition (Critical for Analytics):** Each attribute MUST have defined behavioral criteria for 4 score ranges:
  - **1-5 (Low):** Behaviors indicating poor performance
  - **6-10 (Developing):** Learning, needs improvement
  - **11-15 (Proficient):** Competent, meets expectations
  - **16-20 (Exceptional):** Mastery, exceeds expectations
- **Data Sources:** Each attribute specifies how it's measured (360° Feedback, Manager Eval, Skills Test, etc.)
- **Weight:** Attributes have Weight (Low/Medium/High) affecting Fit Score calculations
- **No Zone:** Zone is at department level only, not attribute level

---

## Acceptance Criteria

### Scenario 1: View Attribute with Scale Definition

**Given**
- Club Owner is on Attribute Library page
- Attribute "Leadership" exists

**When**
- Owner clicks on the Leadership card

**Then**
- System displays Attribute Detail modal
- Modal shows Overview: Category, Description, Weight
- Modal shows Data Sources with Primary highlighted
- Modal shows Scale Definition (1-20) with 4 levels:
  - 🔴 1-5 LOW with specific behavioral indicators
  - 🟡 6-10 DEVELOPING with specific criteria
  - 🟢 11-15 PROFICIENT with specific criteria
  - 🔵 16-20 EXCEPTIONAL with mastery indicators

---

### Scenario 2: Create Attribute with Scale Definition

**Given**
- Owner clicks "+ Add Attribute"
- Add Attribute modal opens with 3 tabs

**When**
- Owner fills Basic Info (Name, Category, Description, Weight, Icon)
- Owner goes to Scale Definition tab
- Owner defines behavioral criteria for each score range
- Owner goes to Data Sources tab
- Owner selects Primary and Secondary sources
- Owner clicks "Save Attribute"

**Then**
- System creates attribute with all scale definitions
- Attribute appears in correct category section
- Scale definitions are stored for analytics use

---

### Scenario 3: Search and Filter Attributes

**Given**
- Owner is on Attribute Library page
- Many attributes exist across categories

**When**
- Owner types in search box or selects category filter

**Then**
- List filters to show matching attributes only
- Category sections expand/collapse as needed

---

## UI/UX Notes

**Screens Involved:**
1. **Attribute Library Page** ([03-attribute-library.html](file:///Users/gdrom/Desktop/allkons/ascend-hr-docs/ascendhr/design/formation-view/03-attribute-library.html))

**Key UI Elements:**
- **Stats Row:** Total, Core, Technical, Business counts
- **Filter Bar:** Search input + Category dropdown
- **Category Accordions:** Collapsible sections for each category
- **Attribute Cards:** Icon, Name, Description, Source, Weight badge
- **Detail Modal:** Overview, Data Sources, Scale Definition (4 levels)
- **Add/Edit Modal (3 tabs):**
  - Basic Info: Name, Category, Description, Weight, Icon
  - Scale Definition: 4 text areas for each score range
  - Data Sources: Primary dropdown + Secondary checkboxes

**Scale Definition Colors:**
- 🔴 1-5 LOW: Red (#FEE2E2, #DC2626)
- 🟡 6-10 DEVELOPING: Yellow (#FEF3C7, #D97706)
- 🟢 11-15 PROFICIENT: Green (#D1FAE5, #059669)
- 🔵 16-20 EXCEPTIONAL: Blue (#DBEAFE, #2563EB)

---

## Data Model

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| id | UUID | Yes | Unique identifier |
| name | String | Yes | Attribute name |
| icon | String | No | Emoji icon |
| category | Enum | Yes | core, technical, business, creative |
| description | String | Yes | What attribute measures |
| weight | Enum | Yes | low (×1.0), medium (×1.25), high (×1.5) |
| primary_source | Enum | Yes | How measured primarily |
| secondary_sources | Array | No | Additional measurement methods |
| scale_low | Text | Yes | Behaviors for 1-5 |
| scale_developing | Text | Yes | Behaviors for 6-10 |
| scale_proficient | Text | Yes | Behaviors for 11-15 |
| scale_exceptional | Text | Yes | Behaviors for 16-20 |
