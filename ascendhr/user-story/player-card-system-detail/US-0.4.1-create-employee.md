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

เมื่อ HR สร้างพนักงานใหม่ ระบบจะต้องสร้างทั้ง Employee record และ User account พร้อมกัน จากนั้นจะส่งอีเมลเชิญให้พนักงานตั้งรหัสผ่านเพื่อเข้าใช้งานระบบ

Player Card ของพนักงานจะประกอบด้วย:
- ข้อมูลพื้นฐาน (ชื่อ, อีเมล, แผนก, ตำแหน่ง)
- รูปโปรไฟล์
- Attributes 10 ค่า (1-20 คะแนน)
- Current Ability (คำนวณจาก Attributes)
- Potential Ability (ต้อง ≥ Current Ability)

**Key Business Rules:**
- Email ต้องไม่ซ้ำในระบบ
- รูปโปรไฟล์ต้องไม่เกิน 5MB
- Potential Ability ต้องมากกว่าหรือเท่ากับ Current Ability
- ต้องมี Departments และ Positions ในระบบก่อน

---

## Acceptance Criteria

### Scenario 1: Successfully Create Employee with Player Card

**Given**
- Scout is logged in with `employee:create` permission
- Departments and Positions already exist in the system

**When**
- Scout clicks "Add Employee" button
- Scout fills all required fields (name, email, department, position)
- Scout uploads profile photo (optional)
- Scout sets "Reports To" manager (optional)
- Scout rates 10 attributes using 1-20 sliders
- Scout sets Potential Ability ≥ Current Ability
- Scout clicks "Create Player"

**Then**
- System creates employee record in database
- System auto-creates user account with generated password
- System sends invitation email to employee
- System shows success message with link to Player Card
- Current Ability is calculated from the 10 attributes

---

### Scenario 2: Email Already Registered

**Given**
- Scout is on the Create Employee form
- An employee with email "john@company.com" already exists

**When**
- Scout enters "john@company.com" in email field
- Scout attempts to submit the form

**Then**
- System shows error "Email already registered"
- Form remains open for correction
- No employee record is created

---

### Scenario 3: Photo Exceeds Size Limit

**Given**
- Scout is on the Create Employee form
- Scout has filled all required fields

**When**
- Scout uploads a profile photo that is larger than 5MB

**Then**
- System shows error "Photo must be under 5MB"
- Photo is rejected and not uploaded
- Form remains open for correction

---

### Scenario 4: Potential Less Than Current Ability

**Given**
- Scout is on the Create Employee form
- Scout has rated attributes resulting in Current Ability of 15

**When**
- Scout sets Potential Ability to 12 (less than Current)
- Scout attempts to submit

**Then**
- System shows error "Potential must be ≥ Current Ability"
- Form remains open for correction

---

### Scenario 5: Form Validation Fails

**Given**
- Scout is on the Create Employee form

**When**
- Scout leaves required fields empty (name, email, department, position)
- Scout attempts to submit

**Then**
- System highlights all invalid/empty required fields
- System shows field-level validation errors
- Form stays on the same page
- No employee record is created

---

## UI/UX Notes

**Screens Involved:**
1. Employee List (with "Add Employee" button)
2. Create Employee Form
3. Attribute Rating Panel (sliders + radar chart preview)
4. Success Confirmation (with Player Card preview)

**Key UI Elements:**
- **Add Employee Button**: Primary action on Employee List page
- **Basic Info Form**: Name, Email, Department (dropdown), Position (dropdown)
- **Photo Upload**: Drag-drop zone with preview, max 5MB indicator
- **Reports To Dropdown**: Searchable manager selector
- **Attribute Sliders**: 10 sliders with 1-20 range, real-time radar chart update
- **Current Ability Display**: Auto-calculated from attributes (read-only)
- **Potential Ability Slider**: Must be ≥ Current Ability
- **Create Player Button**: Primary submit action
