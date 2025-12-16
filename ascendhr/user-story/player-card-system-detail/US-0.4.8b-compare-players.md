# Compare Players

**Story ID:** US-0.4.8b  
**Epic:** 0.4 - Player Card System  
**Persona:** Manager (CEO)

---

## User Story

> **As a** Manager (CEO),  
> **I want to** compare two or more Player Cards side-by-side,  
> **So that** I can make informed decisions about promotions or team composition.

---

## Business Requirement/Logic

Manager ต้องการเปรียบเทียบพนักงานหลายคนพร้อมกันเพื่อ:
- ตัดสินใจเลื่อนตำแหน่ง
- เปรียบเทียบ candidates สำหรับโปรเจค
- วิเคราะห์จุดแข็ง/จุดอ่อนของแต่ละคน

**Key Business Rules:**
- เปรียบเทียบได้สูงสุด 4 คนพร้อมกัน
- ต้องเลือกอย่างน้อย 2 คนถึงจะ compare ได้
- แสดง attributes แบบ side-by-side พร้อม highlight ความแตกต่าง
- Green = ค่าสูงกว่า, Red = ค่าต่ำกว่า
- สามารถ export เป็น image/PDF ได้

---

## Acceptance Criteria

### Scenario 1: Successfully Compare Two Players

**Given**
- Manager is logged in with `employee:read` permission
- Employees "John" and "Jane" exist with rated attributes

**When**
- Manager navigates to Player Gallery
- Manager selects John (checkbox appears, badge shows "1 selected")
- Manager selects Jane (badge shows "2 selected")
- Manager clicks "Compare Selected"

**Then**
- System opens comparison modal
- Shows John and Jane's Player Cards side-by-side
- Each card displays: photo, basic info, radar chart, all attributes
- Attribute differences are highlighted:
  - Higher value = green text/background
  - Lower value = red text/background
- Overall ability comparison is shown

---

### Scenario 2: Compare Up to Four Players

**Given**
- Manager has selected 3 employees in the gallery

**When**
- Manager selects a 4th employee
- Manager clicks "Compare Selected"

**Then**
- System opens comparison modal with 4 cards
- Layout adjusts to fit 4 cards (smaller cards or scrollable)
- All comparisons work correctly across 4 players

---

### Scenario 3: Cannot Add Fifth Player

**Given**
- Manager has already selected 4 employees

**When**
- Manager tries to select a 5th employee

**Then**
- System shows message "Maximum 4 players for comparison"
- 5th selection is not added
- Manager must deselect one before adding another

---

### Scenario 4: Compare Button Disabled with Single Selection

**Given**
- Manager is on Player Gallery
- Manager has selected only 1 employee

**When**
- Manager looks at the "Compare Selected" button

**Then**
- Button is disabled/grayed out
- Tooltip shows "Select at least 2 players to compare"

---

### Scenario 5: Export Comparison

**Given**
- Manager is viewing comparison modal with 3 selected players

**When**
- Manager clicks "Export" button
- Manager selects export format (Image or PDF)

**Then**
- System generates comparison as selected format
- File is downloaded to Manager's device
- Export includes: all player cards, attribute comparison table

---

### Scenario 6: Close Comparison and Return to Gallery

**Given**
- Manager is viewing comparison modal

**When**
- Manager clicks "Close" button

**Then**
- Modal closes
- Manager returns to Player Gallery
- Previous selections are cleared

---

## UI/UX Notes

**Screens Involved:**
1. Player Gallery (with selection checkboxes)
2. Comparison Bar (shows selected count)
3. Comparison Modal (side-by-side view)
4. Attribute Difference Highlights
5. Export Options Panel

**Key UI Elements:**
- **Selection Checkbox**: Overlay on each card, shows when hovering or when any card selected
- **Selection Badge**: Shows count like "2 selected" with avatar stack
- **Comparison Bar**: Floating bar at bottom with "Compare" button and clear action
- **Comparison Modal**: Full-screen or large modal with horizontal card layout
- **Side-by-Side Layout**: 2 cards = 50% each, 3 cards = 33%, 4 cards = 25% or scrollable
- **Difference Highlighting**: Green/red background or text color for better/worse values
- **Radar Chart Overlay**: Option to overlay all radar charts semitransparently
- **Export Button**: Dropdown with "Export as Image" and "Export as PDF" options
- **Close Button**: Top-right corner of modal
