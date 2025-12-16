# Bulk Import Employees

**Story ID:** US-0.4.6  
**Epic:** 0.4 - Player Card System  
**Persona:** Scout (HR)

---

## User Story

> **As a** Scout (HR),  
> **I want to** import multiple employees via CSV,  
> **So that** I can quickly onboard the entire team.

---

## Business Requirement/Logic

เมื่อบริษัทมีพนักงานใหม่จำนวนมาก HR สามารถ import จาก CSV file แทนการสร้างทีละคน ระบบจะ validate ข้อมูลทุกแถวก่อน import และแสดง preview ให้ตรวจสอบก่อน confirm

**Key Business Rules:**
- รองรับเฉพาะไฟล์ CSV
- ระบบให้ download template ที่มี columns ที่ต้องการ
- Validate ทุกแถวก่อน import (email format, required fields, ฯลฯ)
- สามารถ import เฉพาะแถวที่ valid เท่านั้น
- แต่ละพนักงานที่ import สำเร็จจะได้รับ invitation email

---

## Acceptance Criteria

### Scenario 1: Successfully Import Employees

**Given**
- Scout is logged in with `employee:import` permission
- CSV file contains 50 valid employee records

**When**
- Scout clicks "Import Employees"
- Scout downloads template and fills with data (offline)
- Scout uploads the filled CSV file
- System validates all rows and shows all 50 as valid (green)
- Scout reviews the preview
- Scout clicks "Import Valid Rows"

**Then**
- System creates 50 employee records
- System creates 50 user accounts
- System sends 50 invitation emails
- System shows summary: "50 created, 0 skipped, 0 errors"
- Newly imported employees appear in the Employee List

---

### Scenario 2: Wrong File Format

**Given**
- Scout is on the Import Wizard

**When**
- Scout uploads an Excel file (.xlsx) instead of CSV

**Then**
- System shows error "Please upload CSV file"
- File is rejected
- Import wizard stays on upload step

---

### Scenario 3: All Rows Invalid

**Given**
- Scout has uploaded a CSV file
- All rows have validation errors (e.g., missing required fields, invalid emails)

**When**
- System validates the file

**Then**
- System shows all rows in preview as invalid (red)
- "Import Valid Rows" button is disabled
- Scout can click on each row to see specific error details
- System shows message "All rows have errors. Please fix and re-upload."

---

### Scenario 4: Some Rows Valid, Some Invalid

**Given**
- Scout has uploaded a CSV with 50 rows
- 40 rows are valid, 10 rows have errors

**When**
- System validates the file

**Then**
- System shows preview with:
  - 40 valid rows (green indicator)
  - 10 invalid rows (red indicator)
- Scout can click invalid rows to see error details
- "Import Valid Rows" button is enabled
- System shows "40 valid, 10 with errors"

**When**
- Scout clicks "Import Valid Rows"

**Then**
- System imports only the 40 valid rows
- System shows summary: "40 created, 10 skipped"
- Invalid rows are available in error report for correction

---

### Scenario 5: View Row Error Details

**Given**
- Scout is viewing the validation preview
- Row 5 is marked as invalid

**When**
- Scout clicks on Row 5

**Then**
- System displays error detail panel showing:
  - Row number: 5
  - Errors: "Email 'invalid-email' is not valid", "Department 'XYZ' not found"
- Scout understands what needs to be fixed

---

## UI/UX Notes

**Screens Involved:**
1. Import Wizard (step indicator: Template → Upload → Preview → Complete)
2. Template Download Section
3. File Upload Zone (drag-drop)
4. Validation Preview Table (valid/invalid highlighting)
5. Error Detail Panel
6. Import Summary (success/skip/error counts)

**Key UI Elements:**
- **Step Indicator**: Shows progress through import wizard
- **Download Template Button**: Downloads CSV template with headers
- **Drag-Drop Zone**: File upload area with visual feedback
- **Preview Table**: Shows all rows with validation status icons
- **Row Status Indicator**: ✓ green for valid, ✗ red for invalid
- **Error Detail Panel**: Slide-out panel showing specific errors for selected row
- **Import Button**: "Import Valid Rows" with count (e.g., "Import 40 Rows")
- **Summary Card**: Shows created/skipped/error counts with icons
