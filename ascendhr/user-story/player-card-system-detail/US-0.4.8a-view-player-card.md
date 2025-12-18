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

Manager (CEO) needs to view detailed Player Cards to assess talent. The Player Card must visualize attributes using an FC26-inspired design.

**Key Business Rules:**
- **Access:** Requires `employee:read` permission.
- **Card Design:** FC26 style with Tiers (Gold >90, Silver >80, Bronze <80).
- **Attributes:** Displayed via Radar Chart (10 attributes) and 1-99 Score.
- **History:** Track changes over time.
- **Visuals:** Avatar, Club Crest, Position, Flag.

---

## Acceptance Criteria

### Scenario 1: Successfully View Player Card from Gallery

**Given**
- Manager is on the Player Gallery page
- "Alex Chen" exists as a Tech Lead with Rating 95 (Gold Tier)

**When**
- Manager clicks on "Alex Chen's" Gold Card

**Then**
- System navigates to Player Detail page
- Displays full FC26 Player Card component:
  - Gold border/background styling
  - Overall Rating: 95
  - Position: Tech Lead
  - Interactive Radar Chart with 10 attributes
- Background shows club colors/theme

---

### Scenario 2: View Employee Without Attributes

**Given**
- Manager is on the Player Gallery page
- "New Hire" exists but has no rated attributes

**When**
- Manager navigates to "New Hire's" detail page

**Then**
- System displays Player Card in "Unrated" state (Ghost/Grey style)
- Overall Rating shows "—" or "N/A"
- Radar chart displays "Not yet rated" placeholder
- "Rate Player" CTA is visible (if user has permission)

---

### Scenario 3: View Attribute History

**Given**
- Manager is viewing a Player Card
- The player has had previous attribute updates

**When**
- Manager switches to "History" tab

**Then**
- System displays a timeline of changes
- Shows Old Value → New Value (e.g., Pace: 75 → 78)
- Shows Date and User who made the change

---

### Scenario 4: Card Visual Tiers

**Given**
- Player Gallery is loaded

**When**
- Manager views different players

**Then**
- Players with Rating 90+ appear as **Gold** cards (Gold border/glow)
- Players with Rating 80-89 appear as **Silver** cards (Silver border)
- Players with Rating <80 appear as **Bronze** cards (Bronze border)
- Hovering a card triggers a "lift" animation (transform: translateY)

---

## UI/UX Notes

**Screens Involved:**
1. **Player Gallery** (Grid of cards)
2. **Player Detail** (Full card view)

**Key UI Elements:**
- **FC Card:** Tiered styles (Gold/Silver/Bronze) defined in CSS.
- **Rating Badge:** Large number (1-99) with star.
- **Avatar:** Circular profile picture.
- **Radar Chart:** Visualizes attributes like Pace, Shooting, etc. (mapped to business skills).
