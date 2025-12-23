# View & Update Employee (Update Attributes Flow)

**Story ID:** US-0.4.3  
**Epic:** 0.4 - Player Card System  
**Persona:** Scout (HR)

---

## User Story

> **As a** Scout (HR),  
> **I want to** view and update an employee's Player Card attributes,  
> **So that** I can track their growth and maintain accurate skill profiles.

---

## Business Requirement/Logic

Employee Detail page มี **Hero Layout** โดย Spider Chart เป็นองค์ประกอบหลัก:

### Hero Section
- Spider Chart ขนาดใหญ่เปรียบเทียบ actual vs position requirements
- Fit Score แสดงชัดเจน (92%)
- Gap Analysis (Above/Meets/Below)

### Update Attributes Flow (3-Step Wizard)
เมื่อ HR ต้องการ update attributes จะใช้ 3-step wizard:

1. **Step 1: Trigger Selection** - เลือกเหตุผลของการ update
   - Performance Review, Training, Project, Observation, Peer Feedback
   
2. **Step 2: Attribute Adjustment**
   - Sliders แสดง current vs new value
   - ▲+X / ▼-X indicators
   - Justification field สำหรับแต่ละ attribute
   
3. **Step 3: Impact Preview**
   - Before/After fit score comparison
   - Changes summary
   - Evidence link (optional)

**Key Business Rules:**
- ทุกการ update ต้องเลือก trigger type (for analytics)
- Justification แนะนำให้กรอก (for audit trail)
- ประวัติการเปลี่ยนแปลง save ทุกครั้ง

---

## Acceptance Criteria

### Scenario 1: Successfully Update Attributes

**Given**
- Scout is logged in with `employee:update` permission
- Employee exists with Leadership: 15, Technical: 17

**When**
- Scout opens Player Card detail page
- Scout views Hero spider chart and Fit Score (92%)
- Scout clicks "📊 Update Attributes" button
- Scout selects "Performance Review" as trigger (Step 1)
- Scout adjusts Leadership: 15 → 17  
- Scout adds justification "Led Q4 initiative successfully" (Step 2)
- Scout views impact preview: 85% → 92% fit score (Step 3)
- Scout clicks "Confirm & Save"

**Then**
- System saves new attribute values
- System records trigger type, justification, and timestamp
- System updates player card with new values
- History shows update with full metadata

---

### Scenario 2: Preview Without Changes

**Given**
- Scout is on Step 2 of Update Attributes wizard

**When**
- Scout does not move any sliders
- Scout clicks "Preview Impact"

**Then**
- Step 3 shows "No changes made"
- Fit score shows same before/after value
- Confirm button still works (allows saving with trigger only)

---

### Scenario 3: Cancel Update Flow

**Given**
- Scout is on any step of Update Attributes wizard

**When**
- Scout clicks "Cancel"

**Then**
- Modal closes
- No changes are saved
- Player card shows original values

---

## UI/UX Notes

**Screens Involved:**
1. Player Card Detail (Hero layout with spider chart)
2. Update Wizard Step 1: Trigger Selection (5 options)
3. Update Wizard Step 2: Attribute Adjustment (sliders + justification)
4. Update Wizard Step 3: Impact Preview (before/after + summary)

**Key UI Elements:**
- **Hero Spider Chart**: Large, central, shows position requirements vs actual
- **Fit Score Badge**: 92% with color coding
- **Update Attributes Button**: Primary blue action
- **Trigger Options**: Cards with icons for each trigger type
- **Attribute Adjustment Cards**: Slider + old/new values + diff indicator + justification
- **Impact Preview**: Side-by-side before/after fit scores
- **Changes Summary**: List of changed attributes with justifications

**HTML Mockup:** [03-employee-detail.html](file:///Users/gdrom/Desktop/allkons/ascend-hr-docs/ascendhr/design/player-card-system/03-employee-detail.html)
