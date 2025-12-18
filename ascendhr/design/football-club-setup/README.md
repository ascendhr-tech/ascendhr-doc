# Football Club Setup - UI Mockups

**Source:** 
- User Stories: `/ascendhr/user-story/football-club-setup.md`
- UX Flows: `/ascendhr/ux/football-club-setup/`
- Design System: `/ascendhr/design/design-system.md`

**Purpose:** HTML mockups for developer reference  
**Version:** 2.0  
**Updated:** December 16, 2024

> ⚠️ **Note:** Player Card setup (Owner's first card) is now handled in **Epic 0.4 (Player Card System)**. See `/ascendhr/design/player-card-system/` for Player Card mockups.

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
| `03-invite-team.html` | Invite Modal, Confirmation, Accept Flow | US-0.0.3 |

---

## Flow Overview

```
Landing → Register → Verify Email → Create Club → Invite Squad (optional) → Dashboard
                                                                              ↓
                                                       (Epic 0.4) Setup Player Card
```

---

## Screen Inventory

| # | Screen | File | Key Components |
|---|--------|------|----------------|
| 1 | Landing Page | 01 | Hero section, "Start Your Journey" CTA |
| 2 | Registration Form | 01 | Name/Email/Password inputs, validation |
| 3 | Email Verification Pending | 01 | Instructions, resend button |
| 4 | Email Verified Success | 01 | Welcome message, auto-redirect |
| 5 | Create Club Wizard - Basic Info | 02 | Club name, industry, size selectors |
| 6 | Create Club Wizard - Branding | 02 | Logo upload, color pickers |
| 7 | Club Created Success | 02 | Confirmation, Invite Team or Dashboard buttons |
| 8 | Invite Team Modal | 03 | Email input, role selector |
| 9 | Invitation Sent Confirmation | 03 | Summary, pending list |
| 10 | Accept Invitation Page | 03 | Welcome, password form (invitee) |
| 11 | Set Password Page | 03 | Password creation (invitee) |

---

## Related Features

| Feature | Epic | Link |
|---------|------|------|
| **Player Card System** | Epic 0.4 | `/ascendhr/design/player-card-system/` |
| **Formation View** | Epic 0.5 | `/ascendhr/design/formation-view/` |

---

## Developer Notes

- All styles use design-system.md tokens
- Gamification elements (Player Card, Tier Badges, Attribute Bars) from Section 8
- Sample data is provided (replace with real data)
- Forms show validation states
- FM (Football Manager) style UI terminology used
- **Player Card setup moved to Epic 0.4** - This epic focuses only on club creation and team invites
