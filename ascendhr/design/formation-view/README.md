# Formation View - UI Mockups

**Epic:** 0.5: Formation View + Squad Builder  
**Source:** 
- User Stories: `/ascendhr/user-story/formation-view.md`
- UX Flows: `/ascendhr/ux/formation-view/`
- Screen Specs: `/ascendhr/ux/formation-view/screen-specs.md`

**Purpose:** HTML mockups for developer reference - Gamified org structure visualization

---

## Quick Start for Developers

1. Open any `.html` file in browser
2. View design and layout
3. **All styles use `../_shared/base.css`** (centralized)
4. Matches mood/tone of `football-club-setup`

---

## HTML Files

| File | Screens | User Stories |
|------|---------|--------------|
| `01-department-management.html` | Department List, Add/Edit Modal | US-0.5.1 |
| `02-position-management.html` | Position List, Config Modal | US-0.5.2 |
| `03-attribute-library.html` | Attribute Library, Add Form | US-0.5.3 |
| `04-role-templates.html` | Template Gallery, Detail View | US-0.5.4 |
| `05-formation-pitch.html` | **Formation Pitch Canvas** (Hero) | US-0.5.5 |
| `06-squad-builder.html` | Squad Dashboard, Builder Canvas | US-0.5.6 |

---

## Zone Color Reference

| Zone | Color | Hex | Usage |
|------|-------|-----|-------|
| Attack | 🔴 Red | `#EF4444` | Sales, Marketing, BD |
| Midfield | 🟢 Green | `#22C55E` | Engineering, Product, Design |
| Defense | 🔵 Blue | `#3B82F6` | Finance, Legal, Ops |
| Support | 🟣 Purple | `#A855F7` | HR, Admin, IT Support |

---

## Developer Notes

- All styles link to `../_shared/base.css`
- Pitch uses green gradient background
- Zone badges use semantic colors
- Player cards show fit scores (high=green, medium=yellow, low=red)
- Modals use standard modal-overlay/modal pattern
- Sidebar navigation consistent across all pages
