# Football Club Setup - UI Mockups

**Source:** 
- User Stories: `/ascendhr/user-story/football-club-setup.md`
- UX Flows: `/ascendhr/ux/football-club-setup/`
- Design System: `/ascendhr/design/design-system.md`

**Purpose:** HTML mockups for developer reference

---

## Quick Start for Developers

1. Open any `.html` file in browser
2. View design and layout
3. Use as reference for React/Next.js implementation
4. All styles follow design-system.md

---

## HTML Files

| File | Screens | User Story |
|------|---------|------------|
| `01-landing-registration.html` | Landing, Registration, Email Verification | US-0.0.1 |
| `02-create-club.html` | Club Creation Wizard (2 steps), Success | US-0.0.2 |
| `03-player-card-setup.html` | Player Card Form, Attributes, Success | US-0.0.3 |
| `04-invite-team.html` | Invite Modal, Confirmation, Accept Flow | US-0.0.4 |

---

## Flow Overview

```
Landing → Register → Verify Email → Create Club → Setup Player Card → Invite Team → Dashboard
```

---

## Developer Notes

- All styles use design-system.md tokens
- Gamification elements (Player Card, Tier Badges, Attribute Bars) from Section 8
- Sample data is provided (replace with real data)
- Forms show validation states
- FM (Football Manager) style UI terminology used
