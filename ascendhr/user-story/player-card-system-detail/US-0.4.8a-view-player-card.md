# View Player Card

**Story ID:** US-0.4.8a  
**Epic:** 0.4 - Player Card System  
**Persona:** Manager (CEO)

---

## User Story

> **As a** Manager (CEO),  
> **I want to** view an employee's Player Card,  
> **So that** I can assess their skills at a glance.

---

## Business Requirement/Logic

Manager (CEO) ต้องการดู Player Card ของพนักงานเพื่อประเมินความสามารถก่อนตัดสินใจเรื่อง:
- การเลื่อนตำแหน่ง
- การจัดทีม
- การมอบหมายงานสำคัญ

Player Card แสดงข้อมูลแบบ Football Manager:
- รูปโปรไฟล์และข้อมูลพื้นฐาน
- Radar Chart แสดง 10 attributes
- Current Ability vs Potential Ability
- ประวัติการเปลี่ยนแปลง attributes

**Key Business Rules:**
- ต้องมี `employee:read` permission
- ถ้า employee ยังไม่มี attributes, แสดง "Not yet rated"
- สามารถดูประวัติการเปลี่ยนแปลงได้
- Player Gallery แสดง cards แบบ grid view

---

## Acceptance Criteria

### Scenario 1: Successfully View Player Card

**Given**
- Manager is logged in with `employee:read` permission
- Employee "John Doe" exists with rated attributes

**When**
- Manager navigates to Player Gallery
- Manager clicks on John Doe's card

**Then**
- System displays full Player Card view with:
  - Profile photo and basic info (name, position, department)
  - Radar chart showing all 10 attributes
  - Current Ability score (displayed prominently)
  - Potential Ability score
  - Status badge (Active, On Leave, etc.)
- All information is read-only for Manager

---

### Scenario 2: View Employee Without Attributes

**Given**
- Manager is viewing Player Gallery
- Employee "Jane New" exists but has not been rated yet

**When**
- Manager clicks on Jane's card

**Then**
- System displays Player Card with basic info
- Radar chart area shows "Not yet rated" message
- Current/Potential Ability shows as "—" or "N/A"
- Prompt suggests contacting HR for attribute rating

---

### Scenario 3: View Attribute History Timeline

**Given**
- Manager is viewing John Doe's Player Card
- John has been rated and updated multiple times

**When**
- Manager clicks on "History" tab

**Then**
- System displays attribute change timeline:
  - Date of each update
  - Which attributes changed (old → new values)
  - Who made the change
- Timeline is sorted newest first
- Can filter by date range

---

### Scenario 4: Navigate Player Gallery

**Given**
- Manager is logged in with `employee:read` permission
- 50 employees exist in the system

**When**
- Manager navigates to Player Gallery

**Then**
- System displays employee cards in grid layout
- Each card shows: photo, name, position, Current Ability score
- Cards are clickable to view full Player Card
- Gallery supports search and filter

---

## UI/UX Notes

**Screens Involved:**
1. Player Gallery (card grid)
2. Player Card Full View
3. Radar Chart Component
4. Attribute History Timeline

**Key UI Elements:**
- **Player Gallery Grid**: 3-4 cards per row, responsive layout
- **Mini Card**: Photo, name, position, ability score badge
- **Full Player Card**: FM-style layout with photo, info panel, radar chart
- **Radar Chart**: 10-axis spider chart with color fill
- **Ability Scores**: Large prominent display of Current/Potential
- **History Tab**: Timeline component with expandable entries
- **Status Badge**: Color-coded (green=Active, yellow=On Leave, red=Terminated)
- **Not Rated State**: Ghost radar chart with "Not yet rated" overlay
