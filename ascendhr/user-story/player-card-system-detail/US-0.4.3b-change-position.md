# Change Position/Department (Transfer Flow)

**Story ID:** US-0.4.3b  
**Epic:** 0.4 - Player Card System  
**Persona:** Scout (HR)

---

## User Story

> **As a** Scout (HR),  
> **I want to** change an employee's position or department,  
> **So that** I can track promotions, demotions, lateral moves, and department transfers like player transfers in football.

---

## Business Requirement/Logic

เมื่อ HR ต้องการเปลี่ยนตำแหน่ง/แผนกของพนักงาน ระบบจะใช้ **4-Step Wizard**:

### Step 1: Change Type Selection
เลือกประเภทการเปลี่ยนแปลง:
- ⬆️ Promotion - เลื่อนตำแหน่งสูงขึ้น
- ↔️ Lateral Move - เปลี่ยน role ระดับเดียวกัน
- 🔄 Department Transfer - ย้ายแผนก (zone)
- ⬇️ Demotion - ลดตำแหน่ง

### Step 2: New Position Selection
- เลือกแผนกใหม่ (แสดง zone color change)
- เลือกตำแหน่งใหม่ (cascading dropdown)
- เลือก manager ใหม่
- กำหนด effective date

### Step 3: Fit Score Comparison
- แสดง Current Role (92%) vs New Role (72%)
- Gap Analysis: แสดง attributes ที่ exceeds (✅) และ gaps (⚠️)
- Development Recommendations: แนะนำ training ที่ต้องการ

### Step 4: Confirmation
- สรุป FROM → TO
- กรอกเหตุผลการเปลี่ยนแปลง
- แนบเอกสารอนุมัติ (optional)

**Key Business Rules:**
- ต้องเลือก change type เพื่อ analytics
- Zone color เปลี่ยนเมื่อย้ายแผนก
- Fit score คำนวณใหม่สำหรับ role ใหม่
- บันทึกประวัติการเปลี่ยนตำแหน่งทุกครั้ง

---

## Acceptance Criteria

### Scenario 1: Successfully Change Position (Lateral Move)

**Given**
- Scout is logged in with `employee:update` permission
- Employee "Alex Chen" is Tech Lead in Engineering (Midfield zone, 92% fit)

**When**
- Scout clicks "🔄 Change Position" button
- Scout selects "Lateral Move" (Step 1)
- Scout selects "Product" department (Attack zone)
- Scout selects "Product Manager" position
- Scout sets effective date to Jan 15, 2025 (Step 2)
- Scout views Fit Score: 92% → 72% (Step 3)
- Scout views Gap Analysis showing Communication gap
- Scout enters reason "Career development interest" (Step 4)
- Scout clicks "Confirm Change"

**Then**
- System updates employee's department and position
- System records change type, old/new positions, effective date
- History shows position change with full metadata
- Employee's zone color changes on Player Card

---

### Scenario 2: Promotion with High Fit Score

**Given**
- Scout selects "Promotion" as change type

**When**
- Scout selects a higher-level position in same department
- New role Fit Score is 88%

**Then**
- Fit Analysis shows mostly green (✅ Exceeds)
- Development Recommendations may be minimal or empty
- Step 3 shows positive fit score change

---

### Scenario 3: Low Fit Score Warning

**Given**
- Scout is on Step 3: Fit Analysis

**When**
- New role Fit Score is below 50%

**Then**
- System shows warning about skill gaps
- Multiple items in Gap Analysis with ⚠️ warnings
- Development Recommendations list multiple required trainings
- Scout can still proceed but is informed of risks

---

### Scenario 4: Cancel Position Change

**Given**
- Scout is on any step of Position Change wizard

**When**
- Scout clicks "Cancel"

**Then**
- Modal closes
- No changes are saved
- Employee retains original position and department

---

## UI/UX Notes

**Screens Involved:**
1. Position Change Wizard Step 1: Change Type Selection
2. Position Change Wizard Step 2: New Position Selection
3. Position Change Wizard Step 3: Fit Score Comparison & Gap Analysis
4. Position Change Wizard Step 4: Confirmation & Reason

**Key UI Elements:**
- **Change Type Cards**: Icons and descriptions for Promotion/Lateral/Transfer/Demotion
- **Current Position Panel**: Shows current dept, position, zone badge
- **Department Dropdown**: Shows zone color for each option
- **Position Dropdown**: Cascades based on department selection
- **Fit Score Comparison**: Side-by-side Current (92%) vs New (72%)
- **Gap Analysis**: Table with attribute, current, required, and gap indicator
- **Development Recommendations**: Bullet list of suggested training
- **Zone Color Change**: Visual FROM → TO with colors

**Data Model:**
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

**HTML Mockup:** [03-employee-detail.html](file:///Users/gdrom/Desktop/allkons/ascend-hr-docs/ascendhr/design/player-card-system/03-employee-detail.html)
