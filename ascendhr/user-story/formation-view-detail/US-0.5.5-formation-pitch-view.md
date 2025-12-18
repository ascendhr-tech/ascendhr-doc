# Formation / Pitch View

**Story ID:** US-0.5.5  
**Epic:** 0.5: Formation View + Squad Builder  
**Persona:** Team Manager  
**Design Reference:** [`05-formation-pitch.html`](file:///Users/gdrom/Desktop/allkons/ascend-hr-docs/ascendhr/design/formation-view/05-formation-pitch.html)

---

## User Story

> **As a** Team Manager,  
> **I want to** view my organization on a football pitch visualization with position-based cards,  
> **So that** I can intuitively understand the team structure, see player distribution per position, and track team health metrics.

---

## Business Requirement/Logic

**Key Business Rules:**

- **Visualization Layout:**
  - Full-width pitch canvas with green gradient background
  - 3 zones on pitch: Attack (top), Midfield (center), Defense (bottom)
  - Bench section (horizontal bar) below pitch for support roles
  - Analytics bar showing team KPIs

- **Position-Based Cards (NOT Player Cards):**
  - Each card represents a **POSITION** (e.g., "Backend Developer")
  - Shows player count in that position (👥 5)
  - Shows average fit score badge (gold/silver/bronze)
  - Click to see list of all players in that position

- **Analytics Bar (5 KPIs):**
  - Team Score (overall health)
  - Coverage % (positions filled)
  - Average Fit Score
  - Strongest Zone (Attack/Mid/Defense)
  - Gaps to Fill (count)

- **Custom Formations Only:**
  - No preset formations (4-3-3, etc.)
  - Users add positions freely to any zone
  - Each zone has unlimited "+" button to add positions

- **Zones:**
  | Zone | Purpose | Color | Example Positions |
  |------|---------|-------|-------------------|
  | Attack (⚔️) | Revenue-generating roles | Red border | PM, Sales Lead |
  | Midfield (⚙️) | Core operations & tech | Blue border | Backend, Frontend, UX |
  | Defense (🛡️) | Support & stability | Green border | Finance, Legal, Ops |
  | Bench (🏠) | Leadership & admin | Purple | CEO, HR, Office Manager |

---

## Acceptance Criteria

### Scenario 1: View Formation with Position Cards

**Given**
- Organization has positions defined with assigned employees
- Zones (Attack/Midfield/Defense/Bench) are configured

**When**
- Manager navigates to "Formation View"

**Then**
- Header shows "Formation View" title
- Analytics bar displays 5 KPIs (Team Score, Coverage, Avg Fit, Strongest Zone, Gaps)
- Pitch renders with 3 zone rows
- Each position shows as a card with:
  - Position abbreviation icon (PM, BE, FE, etc.)
  - Position name
  - Player count (👥 3)
  - Average fit score badge (gold: 80+, silver: 60-79, bronze: <60)
- Zone labels show on left (⚔️ ATK, ⚙️ MID, 🛡️ DEF)
- Bench bar shows below pitch with support positions

---

### Scenario 2: Add New Position to Zone

**Given**
- Manager is viewing the Formation

**When**
- Manager clicks the "+" button in the Midfield zone

**Then**
- Modal opens with "Add Position" title
- Zone selector shows Midfield pre-selected
- Position type grid shows available positions (PM, BE, FE, UX, QA, DevOps)
- Clicking "Add Position" adds the position to the zone
- Zone row updates to show new position card
- Analytics bar updates (total positions count changes)

---

### Scenario 3: View Players in Position

**Given**
- Manager sees a position card with 3 players

**When**
- Manager clicks on the "Backend Developer" position card

**Then**
- Position Details modal opens showing:
  - Position name and zone badge in header
  - Position Overview section:
    - Player count (3)
    - Average Fit Score (87%)
    - Highest individual score (95%)
  - Player List with each employee:
    - Avatar with initials
    - Name
    - Department
    - Individual fit score (color-coded: green/yellow/red)
- "Add Player" button available to assign more employees

---

### Scenario 4: View Team Analytics

**Given**
- Organization has positions and employees assigned

**When**
- Manager views the Formation page

**Then**
- Analytics bar shows:
  | Metric | Example | Trend |
  |--------|---------|-------|
  | Team Score | 85 (green) | ↑ +3 this month |
  | Coverage | 87% (blue) | ↑ 2 filled |
  | Avg Fit | 82% | ↑ +5% |
  | Strongest | Midfield | 5 pos • 89% |
  | Gaps | 2 (warning) | ⚠️ Attention |

---

### Scenario 5: View Stats Summary

**Given**
- Formation has positions in all zones

**When**
- Manager looks at the stats bar at bottom

**Then**
- Stats bar displays:
  - Attack: X pos • Y ppl
  - Midfield: X pos • Y ppl
  - Defense: X pos • Y ppl
  - Bench: X pos • Y ppl
  - Total badge: "Total: 13 positions • 32 employees"

---

## UI/UX Notes

**Screens Involved:**
1. **Formation View Page** (main page)
2. **Add Position Modal**
3. **Position Details Modal** (with player list)

**Key UI Elements:**

| Element | Description |
|---------|-------------|
| Header | "Formation View" title, clean light background |
| Analytics Bar | 5 KPI cards in horizontal grid |
| Pitch Canvas | Green gradient, white pitch markings, center circle |
| Position Card | White card with colored border (red/blue/green), rating badge, position icon |
| Zone Add Button | Circular "+" button at end of each zone row |
| Bench Bar | Light purple horizontal cards |
| Stats Bar | Zone counts with colored dots, total badge |

**Color Scheme:**
- Attack Zone: `#ef4444` (red)
- Midfield Zone: `#3b82f6` (blue)
- Defense Zone: `#22c55e` (green)
- Bench/Support: `#a855f7` (purple)
- Rating Gold: `#f59e0b`
- Rating Silver: `#94a3b8`

**Interactions:**
- Hover on position card → lift + shadow glow
- Click position card → opens Position Details modal
- Click zone "+" button → opens Add Position modal with zone pre-selected
- Click bench "+ Add" → opens Add Position modal with Bench pre-selected
