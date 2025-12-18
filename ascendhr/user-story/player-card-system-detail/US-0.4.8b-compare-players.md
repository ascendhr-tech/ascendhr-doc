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

Efficiency in decision making requires comparing attributes side-by-side. The system provides a floating "Compare Bar" that activates when users select multiple cards.

**Key Business Rules:**
- **Selection:** Cards have a checkmark selection toggle.
- **Max Comparison:** Up to 4 players.
- **Min Comparison:** At least 2 players required to enable "Compare" button.
- **Compare Bar:** Floating bottom bar showing selected avatars and actions.
- **Visuals:** Side-by-side modal with difference highlighting.

---

## Acceptance Criteria

### Scenario 1: Select Players for Comparison

**Given**
- Manager is on the Player Gallery page

**When**
- Manager hovers over a card
- Manager clicks the "Checkmark" (Select) icon on the card

**Then**
- Card displays a green selected border
- "Compare Bar" appears at the bottom of the screen
- Selected player's avatar is added to the Compare Bar
- "Compare" button is initially disabled (if only 1 selected)

---

### Scenario 2: Active Comparison

**Given**
- Manager has selected 2 or more players (up to 4)

**When**
- Manager clicks "Compare Selected" on the Compare Bar

**Then**
- System opens the Comparison Modal
- Selected players are displayed side-by-side
- Attributes are aligned rows for easy scanning
- Higher attributes are highlighted in Green
- Lower attributes are highlighted in Red

---

### Scenario 3: Maximum Limit Enforced

**Given**
- Manager has already selected 4 players

**When**
- Manager attempts to select a 5th player

**Then**
- System prevents selection
- Shows toast/alert: "Maximum 4 players for comparison"

---

### Scenario 4: Clear Selection

**Given**
- Manager has selected players and Compare Bar is visible

**When**
- Manager clicks "Clear" or "Cancel" on the Compare Bar

**Then**
- All cards are deselected
- Compare Bar disappears with specific animation

---

## UI/UX Notes

**Screens Involved:**
1. **Player Gallery** (with active selection state)
2. **Comparison Modal**

**Key UI Elements:**
- **Card Select Toggle:** A small checkbox/circle on the card top-right.
- **Compare Bar:** Fixed bottom bar (z-index high), contains avatars and buttons.
- **Comparison Modal:** Large dialog with standard "Close" button.
- **Attribute Row:** [Label | Player 1 Value | Player 2 Value].
