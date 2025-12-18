# Club Dashboard (Home)

**Story ID:** US-0.0.4  
**Epic:** 0.0 - Football Club Setup  
**Persona:** Club Owner / Manager  
**Design Reference:** [`03-invite-team.html`](file:///Users/gdrom/Desktop/allkons/ascend-hr-docs/ascendhr/design/football-club-setup/03-invite-team.html)

---

## User Story

> **As a** Club Owner,  
> **I want to** see an overview of my club's status and key metrics,  
> **So that** I can quickly understand team health and take action.

---

## Business Requirement/Logic

The Club Dashboard is the main hub after login. It provides a gamified experience inspired by Football Manager with the following components:

**Key Business Rules:**
- Dashboard loads automatically after club creation or login
- Manager Rating updates based on team completeness and fit scores
- Gamification elements (XP, Level, Streak) encourage regular engagement
- KPIs provide at-a-glance team health metrics
- Quick Actions enable fast navigation to key features

---

## Acceptance Criteria

### Scenario 1: View Dashboard After Login

**Given**
- Club Owner has an active club
- At least one department and position exist

**When**
- Club Owner logs in and navigates to Dashboard

**Then**
- Welcome section displays with personalized greeting
- Club name is highlighted in gradient gold
- Manager Rating circle shows current score (0-100)
- Gamification bar shows Level, XP progress, and streak

---

### Scenario 2: View Team KPIs

**Given**
- Club has employees and positions configured

**When**
- Dashboard loads

**Then**
- 4 KPI cards display:
  | KPI | Description |
  |-----|-------------|
  | Squad Size | Total employees (e.g., 12/15 target) |
  | Average Fit | Team-wide average fit score (e.g., 82%) |
  | Vacancies | Open positions needing attention (red if urgent) |
  | Dept Coverage | % of departments with at least 1 employee |

---

### Scenario 3: Use Quick Actions

**Given**
- Club Owner is on Dashboard

**When**
- Club Owner clicks a Quick Action button

**Then**
- System navigates to the corresponding page:
  | Action | Destination |
  |--------|-------------|
  | 🎮 Add New Player | Create Employee form |
  | ⚽ View Formation | Formation Pitch view |
  | 📧 Invite Team | Opens Invite Modal |
  | 📊 View Reports | Analytics/Reports page |

---

### Scenario 4: View Recent Activity

**Given**
- Club has activity history

**When**
- Dashboard loads

**Then**
- Activity feed shows recent events:
  - Player additions
  - Level ups
  - Profile updates
  - Achievements
- Each item shows avatar, description, and timestamp

---

### Scenario 5: View Pending Invites

**Given**
- Club Owner has sent invitations

**When**
- Dashboard loads

**Then**
- Pending Invites section shows:
  - Email address of invitee
  - Role assigned
  - Status badge (Pending/Accepted)
- "Invite Team Members" button available

---

### Scenario 6: Complete Getting Started Checklist

**Given**
- Club Owner is new to the platform

**When**
- Dashboard loads

**Then**
- Getting Started checklist shows:
  - ✅ Create your club (completed)
  - ⬜ Invite your team members
  - ⬜ Set up departments & positions
  - ⬜ Add your first player
- Clicking a checklist item navigates to that feature

---

### Scenario 7: New Club (Empty State)

**Given**
- Club was just created
- No employees exist yet

**When**
- Dashboard loads

**Then**
- Action bar shows "Build your squad starting with yourself!"
- Manager Rating shows low score (e.g., 15%)
- Vacancies KPI highlights urgency
- Quick Actions prioritize "Add New Player"

---

## UI/UX Notes

**Screens Involved:**
1. **Club Dashboard** (single page with multiple components)

**Key UI Elements:**

| Element | Description |
|---------|-------------|
| Welcome Banner | Gradient (blue→purple), greeting, club name in gold, rating circle |
| Gamification Bar | Level badge (gold), XP progress bar, streak flame icon |
| KPI Cards | 4-column grid with icon, value, trend |
| Action Bar | Contextual prompt with primary CTA button |
| Quick Actions | 2x2 icon buttons grid |
| Activity Feed | Timeline of recent actions |
| Pending Invites | List with avatar, email, status badge |
| Getting Started | Checklist with checkmarks |

**Color Scheme:**
- Welcome gradient: `#1e40af → #7c3aed`
- Club name: Gold gradient `#fbbf24 → #f59e0b`
- Level badge: Gold `#fbbf24`
- XP bar: Blue→Purple `#3b82f6 → #7c3aed`
- Streak: Yellow/amber
- Success/good: `#22c55e`
- Warning/urgent: `#f59e0b` or `#ef4444`
