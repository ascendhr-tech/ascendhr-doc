# Setup Owner's Player Card (Dogfooding)

**Story ID:** US-0.0.3  
**Epic:** 0.0 - Football Club Setup  
**Persona:** Club Owner

---

## User Story

> **As a** Club Owner,  
> **I want to** create my own Player Card,  
> **So that** I can experience the system before adding my team.

---

## Business Requirement/Logic

เจ้าของ Club จะต้องสร้าง Player Card ของตัวเองก่อน เพื่อให้ได้ลองใช้งานระบบก่อน (Dogfooding) และเป็น Employee คนแรกใน Club

**Key Business Rules:**
- Owner เป็น Employee คนแรกที่ถูกสร้างใน Club
- ต้องเลือก Position และ Department
- ต้อง rate อย่างน้อย 3 attributes จาก 10 ค่า
- Potential Ability ต้อง ≥ Current Ability
- หลังสร้างสำเร็จ จะแสดง Player Card แบบ FM-style

**10 Attributes ที่ต้อง rate (1-20):**
1. Coding
2. Sales Closing
3. Copywriting
4. Design
5. Data Analysis
6. Leadership
7. Determination
8. Adaptability
9. Teamwork
10. Creativity

---

## Acceptance Criteria

### Scenario 1: Successfully Create Owner's Player Card

**Given**
- Club Owner has created their club
- Owner has no employee/player card yet

**When**
- System displays "Set up your Player Card" prompt
- Owner selects their position (e.g., "CEO")
- Owner selects/creates their department (e.g., "Leadership")
- Owner rates at least 3 attributes using 1-20 sliders
- Owner sets Potential Ability (≥ Current Ability)
- Owner uploads profile photo (optional)
- Owner clicks "Create My Player Card"

**Then**
- System creates Employee record for owner
- System creates Player Card with attributes
- System calculates Current Ability from attributes
- System shows FM-style Player Card preview with radar chart
- System shows "You're ready!" message with next steps
- Owner can proceed to invite team or explore dashboard

---

### Scenario 2: Not Enough Attributes Rated

**Given**
- Club Owner is on the Player Card setup form
- Owner has rated only 2 attributes

**When**
- Owner attempts to submit the form

**Then**
- System shows warning "Rate at least 3 attributes"
- Form remains open for correction
- Submit button is disabled until requirement is met

---

### Scenario 3: Potential Less Than Current Ability

**Given**
- Club Owner is on the Player Card setup form
- System has calculated Current Ability as 15 based on ratings

**When**
- Owner sets Potential Ability to 12 (less than Current)
- Owner attempts to submit

**Then**
- System shows error "Potential must be ≥ Current Ability"
- Potential Ability slider is highlighted
- Form remains open for correction

---

## UI/UX Notes

**Screens Involved:**
1. Setup Player Card Prompt (onboarding step)
2. Player Card Form (with attribute sliders)
3. Radar Chart Preview (live update as sliders change)
4. Player Card Created Success (with FM-style card display)

**Key UI Elements:**
- **Position Dropdown**: CEO, Founder, CTO, COO, etc.
- **Department Selector**: Choose existing or create new
- **Attribute Sliders**: 10 sliders with 1-20 range, grouped by type (Technical/Mental)
- **Radar Chart**: Live preview that updates as sliders move
- **Current Ability Display**: Auto-calculated (read-only)
- **Potential Ability Slider**: Manual input, must be ≥ Current
- **Photo Upload**: Optional, with preview
- **Player Card Preview**: FM-style card showing all info
- **Next Steps Panel**: "Invite your team" and "Explore dashboard" buttons
