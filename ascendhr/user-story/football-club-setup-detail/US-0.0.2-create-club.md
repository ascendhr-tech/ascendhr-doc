# Create Your Club

**Story ID:** US-0.0.2  
**Epic:** 0.0 - Football Club Setup  
**Persona:** Club Owner

---

## User Story

> **As a** Club Owner,  
> **I want to** create my Football Club (company),  
> **So that** I can set up my organization on the platform.

---

## Business Requirement/Logic

หลังจากยืนยัน email แล้ว เจ้าของจะต้องสร้าง Club (บริษัท) ของตนเอง ระบบจะสร้าง:
- Company record ใน database
- กำหนด user เป็น Club Owner (Super Admin)
- สร้าง default departments และ positions

**Key Business Rules:**
- Club name ต้องไม่ซ้ำกับ club อื่นในระบบ
- Logo ต้องมีขนาดไม่เกิน 2MB (รองรับ PNG, JPG, SVG)
- ระบบจะสร้าง slug จากชื่อ club อัตโนมัติ
- User ที่สร้าง club จะกลายเป็น Super Admin โดยอัตโนมัติ
- หลังสร้าง club สำเร็จ จะ redirect ไปหน้า Setup Player Card

---

## Acceptance Criteria

### Scenario 1: Successfully Create Club

**Given**
- Club Owner is logged in and verified
- User has no club yet

**When**
- User lands on "Create Your Club" wizard
- User enters club name (e.g., "Acme Corp")
- User selects industry (e.g., "Technology")
- User selects company size (e.g., "11-50 employees")
- User uploads logo (optional)
- User chooses primary and secondary colors
- User clicks "Create Club"

**Then**
- System validates club name is unique
- System generates slug (e.g., "acme-corp")
- System creates company record in database
- System assigns user as Club Owner (Super Admin role)
- System creates default departments (Leadership, Operations, etc.)
- System redirects to "Setup Your Player Card"
- System shows success message

---

### Scenario 2: Club Name Already Taken

**Given**
- Club Owner is on "Create Your Club" wizard
- A club named "Acme Corp" already exists

**When**
- User enters "Acme Corp" as club name
- System checks uniqueness

**Then**
- System shows error "Name already in use"
- System suggests alternatives (e.g., "Acme Corp 2", "Acme Corporation")
- Form remains open for correction

---

### Scenario 3: Logo Exceeds Size Limit

**Given**
- Club Owner is on "Create Your Club" wizard

**When**
- User uploads a logo file larger than 2MB

**Then**
- System shows error "Logo must be under 2MB"
- Logo is rejected and not uploaded
- Form remains open for correction

---

### Scenario 4: Invalid Logo Format

**Given**
- Club Owner is on "Create Your Club" wizard

**When**
- User uploads a logo in unsupported format (e.g., .gif, .bmp)

**Then**
- System shows error "Please upload PNG, JPG, or SVG"
- File is rejected
- Form remains open for correction

---

## UI/UX Notes

**Screens Involved:**
1. Create Club Wizard (Step 1: Basic Info - name, industry, size)
2. Create Club Wizard (Step 2: Branding - logo, colors)
3. Club Created Success Screen

**Key UI Elements:**
- **Club Name Field**: Text input with uniqueness check on blur
- **Industry Dropdown**: Predefined list of industries
- **Company Size Selector**: Radio buttons or dropdown (1-10, 11-50, 51-200, 200+)
- **Logo Upload Zone**: Drag-drop area with preview
- **Color Pickers**: Primary and secondary color selection with hex input
- **Sample Card Preview**: Live preview of Player Card with selected colors
- **Progress Indicator**: Step 1 of 2, Step 2 of 2
