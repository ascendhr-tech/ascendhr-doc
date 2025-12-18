# Football Club Setup - UX Flow Diagrams

**Source PRD:** `/ascendhr/user-story/football-club-setup.md`  
**Purpose:** Mermaid.js diagrams for v0.dev UI generation  
**Version:** 2.0  
**Updated:** December 16, 2024

> ⚠️ **Note:** Player Card setup (Owner's first card) is now handled in **Epic 0.4 (Player Card System)**. See `/ascendhr/ux/player-card-system/` for Player Card UX flows.

## Usage
1. Copy `.mmd` file content
2. Paste into [mermaid.live](https://mermaid.live)
3. Export as image
4. Use in v0.dev

## Flow Files

| File | User Story | Description |
|------|------------|-------------|
| `00-site-map.mmd` | - | Onboarding navigation structure |
| `01-register-account.mmd` | US-0.0.1 | Owner sign up + email verification |
| `02-create-club.mmd` | US-0.0.2 | Club creation wizard |
| `03-invite-squad.mmd` | US-0.0.3 | Invite team members |

## Screen Inventory

| # | Screen | Used In | Key Components |
|---|--------|---------|----------------|
| 1 | Landing Page | 01 | Hero section, "Start Your Journey" CTA |
| 2 | Registration Form | 01 | Name/Email/Password inputs, validation |
| 3 | Email Verification Pending | 01 | Instructions, resend button |
| 4 | Email Verified Success | 01 | Welcome message, auto-redirect |
| 5 | Create Club Wizard - Basic Info | 02 | Club name, industry, size selectors |
| 6 | Create Club Wizard - Branding | 02 | Logo upload, color pickers |
| 7 | Club Created Success | 02 | Confirmation, next step CTA |
| 8 | Invite Team Modal | 03 | Email input, role selector |
| 9 | Invitation Sent Confirmation | 03 | Summary, pending list |
| 10 | Accept Invitation Page | 03 | Welcome, password form (invitee) |
| 11 | Set Password Page | 03 | Password creation (invitee) |

## Onboarding Flow Summary

```
Landing → Register → Verify Email → Create Club → Invite Squad (optional) → Dashboard
                                                                              ↓
                                                       (Epic 0.4) Setup Player Card
```

## Related Epics

| Epic | Description | Link |
|------|-------------|------|
| **Epic 0.4** | Player Card System (includes Owner's Player Card setup) | `/ascendhr/ux/player-card-system/` |
| **Epic 0.5** | Formation View (Department/Position setup) | `/ascendhr/ux/formation-view/` |
