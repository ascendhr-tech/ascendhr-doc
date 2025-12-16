# Football Club Setup - UX Flow Diagrams

**Source PRD:** `/ascendhr/user-story/football-club-setup.md`  
**Purpose:** Mermaid.js diagrams for v0.dev UI generation

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
| `03-setup-owner-player-card.mmd` | US-0.0.3 | First player card setup (dogfooding) |
| `04-invite-squad.mmd` | US-0.0.4 | Invite team members |

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
| 8 | Setup Player Card Form | 03 | Position/Department, attribute sliders |
| 9 | Radar Chart Preview | 03 | Live radar chart visualization |
| 10 | Player Card Success | 03 | FM-style card display, next steps |
| 11 | Invite Team Modal | 04 | Email input, role selector |
| 12 | Invitation Sent Confirmation | 04 | Summary, pending list |
| 13 | Accept Invitation Page | 04 | Welcome, password form (invitee) |
| 14 | Set Password Page | 04 | Password creation (invitee) |

## Onboarding Flow Summary

```
Landing → Register → Verify Email → Create Club → Setup Player Card → Invite Squad → Dashboard
```
