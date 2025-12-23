# Create Employee + Player Card

**Story ID:** US-0.4.1  
**Epic:** 0.4 - Player Card System  
**Persona:** Scout (HR)

---

## User Story

> **As a** Scout (HR),  
> **I want to** create a new employee with a Player Card,  
> **So that** I can add them to the squad and track their skills.

---

## Business Requirement/Logic

เมื่อ HR สร้างพนักงานใหม่ ระบบจะใช้ **3-Step Wizard** เพื่อนำทางการกรอกข้อมูล:

### Step 1: Basic Info
- ชื่อ, อีเมล, เบอร์โทร

### Step 2: Assignment
- แผนก (มี Zone color: Attack=Red, Midfield=Green, Defense=Blue, Support=Purple)
- ตำแหน่ง (Cascading จากแผนก)
- Reports To Manager

### Step 3: Attributes
- Rate 5 core attributes (1-20)
- แสดง **Spider Chart** เปรียบเทียบค่าที่กรอกกับ Position Requirements
- แสดง **Fit Score** แบบ real-time
- แสดง **Gap Analysis** (Above/Meets/Below)

**Key Business Rules:**
- Email ต้องไม่ซ้ำในระบบ
- ต้องมี Departments และ Positions พร้อม Zone assignments
- Fit Score คำนวณจาก attributes เทียบกับ position requirements

---

## Acceptance Criteria

### Scenario 1: Successfully Create Employee with 3-Step Wizard

**Given**
- Scout is logged in with `employee:create` permission
- Departments and Positions exist with Zone assignments

**When**
- Scout clicks "Add Player" button
- Scout completes Step 1: Basic Info (name, email, phone)
- Scout clicks "Next: Assignment"
- Scout completes Step 2: Assignment (department with zone, position, manager)
- Scout clicks "Next: Attributes"
- Scout rates 5 attributes using sliders
- Scout views spider chart showing position comparison
- Scout views live Fit Score and Gap Analysis
- Scout clicks "Create Player"

**Then**
- System creates employee record with zone assignment
- System shows success with Player Card preview (zone-styled)
- Spider chart and Fit Score update in real-time during input

---

### Scenario 2: Email Already Registered

**Given**
- Scout is on Step 1 of Create Employee wizard
- An employee with email "john@company.com" already exists

**When**
- Scout enters "john@company.com" in email field
- Scout attempts to proceed to next step

**Then**
- System shows error "Email already registered"
- Form remains on Step 1 for correction

---

### Scenario 3: Department Change Updates Position Options

**Given**
- Scout is on Step 2 of Create Employee wizard
- Scout has already selected a department

**When**
- Scout changes department selection

**Then**
- Position dropdown resets
- Position options update to match new department
- Zone badge updates to show new zone color

---

### Scenario 4: Attribute Below Position Requirement

**Given**
- Scout is on Step 3 of Create Employee wizard
- Position requires Leadership: 14

**When**
- Scout sets Leadership attribute to 10

**Then**
- Spider chart shows gap visually (dashed line vs filled area)
- Gap Analysis shows "Below" count increases
- Fit Score decreases accordingly
- Warning indicator shown on slider

---

## UI/UX Notes

**Screens Involved:**
1. Step 1: Basic Information (name, email, phone)
2. Step 2: Assignment (department with zone badge, position, manager)
3. Step 3: Attributes (sliders + spider chart + fit score panel)
4. Live Preview Card (right panel, zone-styled)

**Key UI Elements:**
- **Step Indicator**: 1-2-3 wizard progress
- **Zone Badge**: Color-coded department zone (Attack/Midfield/Defense/Support)
- **Spider Chart**: Dashed line = position requirements, Filled = input values
- **Fit Score Panel**: Percentage with color coding (green=high, red=low)
- **Gap Analysis**: Above/Meets/Below counts
- **Position Requirement Badges**: Show required value next to each slider

**HTML Mockup:** [02-create-employee.html](file:///Users/gdrom/Desktop/allkons/ascend-hr-docs/ascendhr/design/player-card-system/02-create-employee.html)
