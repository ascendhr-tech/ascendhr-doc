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

The system must display all employees as "Player Cards" (FC26 style) in a responsive grid layout. It includes a filter bar for real-time searching and filtering.

**Key Business Rules:**
- **Card View:** Display employees as cards (Gold/Silver/Bronze tiers based on rating).
- **Search:** Real-time filtering by Name or Position.
- **Filters:** Dropdowns for Department and Status.
- **Sorting:** Sort by Rating (High to Low).
- **Interactions:** Clicking a card opens the Employee Detail page.
- **Visuals:** Hover effects should be interactive but not simple underlines.

---

## Acceptance Criteria

### Scenario 1: Successfully View and Search Player Gallery

**Given**
- User is logged in with `employee:read` permission
- There are multiple employees in the system

**When**
- User navigates to "Players" page
- User types "John" in the search box

**Then**
- System displays employees as player cards in a grid
- System filters cards in real-time to show only matches for "John"
- Results count (e.g., "Showing 5 players") updates automatically

---

### Scenario 2: Filter by Department and Status

**Given**
- User is on the Player Gallery page

**When**
- User selects "Engineering" from Department filter
- User selects "Active" from Status filter

**Then**
- System updates the grid to show only Active engineers
- Non-matching cards are hidden

---

### Scenario 3: Sort by Rating

**Given**
- User is on the Player Gallery page

**When**
- User clicks "Sort by Rating" button

**Then**
- System reorders cards by their Overall Rating (Attribute Average) from High to Low

---

### Scenario 4: No Results Found

**Given**
- User is on the Player Gallery page

**When**
- User enters a search term that matches no players

**Then**
- System hides all cards
- Results count shows "Showing 0 players"

---

## UI/UX Notes

**Screens Involved:**
1. **Player Gallery:** Main view with Card Grid.

**Key UI Elements:**
- **Filter Bar:** Contains Search Box, Dept Dropdown, Status Dropdown, Sort Button.
- **Player Card:** Displays Photo, Rating, Position, Name, Flag, Club Crest.
- **Grid Layout:** Responsive grid adapting to screen size.
