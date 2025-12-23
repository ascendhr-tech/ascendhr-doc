# Player Gallery & Search

**Story ID:** US-0.4.2  
**Epic:** 0.4 - Player Card System  
**Persona:** Scout (HR)

---

## User Story

> **As a** Scout (HR),  
> **I want to** search and filter the player gallery,  
> **So that** I can visually browse the squad and find specific players.

---

## Business Requirement/Logic

Player Gallery แสดง employees แบบ **FIFA-style Card Grid** โดยมี:

### Stats Row
- แสดงจำนวนพนักงานทั้งหมดและแยกตาม Zone
- Total Players, Attack (🔴), Midfield (🟢), Defense (🔵), Support (🟣)

### Zone Filter Pills
- Quick filter โดย click ที่ Zone pill
- Update counts และ cards ทันที

### FIFA-style Cards
- Header สีตาม Zone ของพนักงาน
- Overall rating badge
- Position และ Department
- Hover actions: Select (สำหรับ compare), Delete

### Compare Feature
- Select หลาย cards เพื่อเปรียบเทียบ
- Spider chart แสดง side-by-side

**Key Business Rules:**
- ต้อง compare เฉพาะพนักงานใน department เดียวกัน
- Filter ทำงาน real-time

---

## Acceptance Criteria

### Scenario 1: View Player Gallery with Zone Stats

**Given**
- Scout is logged in with `employee:read` permission
- 10 employees exist (2 Attack, 5 Midfield, 2 Defense, 1 Support)

**When**
- Scout navigates to "Players" page

**Then**
- Stats row shows: Total (10), Attack (2), Midfield (5), Defense (2), Support (1)
- All 10 player cards displayed in grid
- Each card has zone-colored header
- Zone badges shown on filter bar

---

### Scenario 2: Filter by Zone

**Given**
- Scout is viewing Player Gallery
- All zones pill is currently active

**When**
- Scout clicks "Midfield" zone pill

**Then**
- Only Midfield zone players shown (5 cards)
- Other zone cards hidden
- Midfield pill shows active state
- Stats row still shows all counts

---

### Scenario 3: Search Players

**Given**
- Scout is viewing Player Gallery

**When**
- Scout types "Alex" in search box

**Then**
- Cards filter in real-time to show only players with "Alex" in name
- No full page reload
- Clear search shows all cards again

---

### Scenario 4: Compare Two Players

**Given**
- Scout is viewing Player Gallery
- Two players from same department exist

**When**
- Scout clicks "Select" on first player card
- Scout clicks "Select" on second player card
- Scout clicks "Compare Selected" button

**Then**
- Compare modal opens
- Side-by-side spider charts shown
- Attribute differences highlighted (green=better, red=worse)

---

### Scenario 5: No Players in Zone

**Given**
- Scout is viewing Player Gallery
- No employees in "Support" zone

**When**
- Scout clicks "Support" zone pill

**Then**
- Empty state shows "No players in this zone"
- Add Player button visible

---

## UI/UX Notes

**Screens Involved:**
1. Player Gallery (Card Grid with zone-colored headers)
2. Stats Row (Total and zone counts)
3. Filter Bar (Zone pills, search, sort dropdown)
4. Compare Modal (side-by-side spider charts)

**Key UI Elements:**
- **Stats Row**: 5 stat cards showing count per zone with colors
- **Zone Pills**: All / Attack / Midfield / Defense / Support filter buttons
- **Player Card**: Zone-colored header, Overall rating, Position badge, Avatar
- **Hover Actions**: Select checkbox, Delete button
- **Compare Bar**: Shows selected count, Compare button
- **Compare Modal**: Two spider charts side-by-side, attribute table with +/- diff

**HTML Mockup:** [04-player-gallery.html](file:///Users/gdrom/Desktop/allkons/ascend-hr-docs/ascendhr/design/player-card-system/04-player-gallery.html)
