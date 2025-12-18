# Football Club Setup - User Stories

**Epic:** 0.0 - Football Club Setup (Multi-tenant)  
**Version:** 3.0  
**Created:** December 16, 2024  
**Updated:** December 18, 2024  
**Purpose:** User stories for UX flow design

> ⚠️ **Note:** Player Card setup (Owner's first card) is now handled in **Epic 0.4 (Player Card System)** since it requires Department/Position to be configured first. See `player-card-system.md` for US-0.4.0.

---

## User Personas

| Persona | Role | Key Actions |
|---------|------|-------------|
| **Club Owner** | CEO/Founder/Business Owner | Register account, create club, view dashboard, invite team |

---

## Design References

| Story | HTML Mockup |
|-------|-------------|
| US-0.0.1 | `01-register-account.html` |
| US-0.0.2 | `02-create-club.html` |
| US-0.0.3 | `03-invite-team.html` (Invite Modal) |
| US-0.0.4 | `03-invite-team.html` (Dashboard) |

---

## US-0.0.1: Register Account (Owner Sign Up)

> **As a** Club Owner,  
> **I want to** create an account on the platform,  
> **So that** I can start my journey to build my squad.

### Scenario
A business owner discovers AscendHR and wants to register to use the Squad Planner for their company.

### Preconditions
- User has a valid email address
- User is not already registered

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Visit landing page | Display "Start Your Journey" CTA |
| 2 | Click "Start Your Journey" | Navigate to registration form |
| 3 | Fill name, email, password | Validate fields in real-time |
| 4 | Click "Create Account" | Submit registration |
| 5 | - | Send verification email |
| 6 | - | Show "Check your email" message |
| 7 | Click link in email | Verify email address |
| 8 | - | Activate account, redirect to "Create Your Club" |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 3a | Email already registered | Show error "Email already in use. Login instead?" |
| 3b | Password too weak | Show error "Password must be at least 8 characters" |
| 7a | Verification link expired | Show error "Link expired" with resend option |

### Screens
1. Landing Page (with "Start Your Journey" CTA)
2. Registration Form
3. Email Verification Pending Screen
4. Email Verified Success Screen

---

## US-0.0.2: Create Your Club

> **As a** Club Owner,  
> **I want to** create my Football Club (company),  
> **So that** I can set up my organization on the platform.

### Scenario
After registering, the owner creates their company profile using the Football Manager-inspired wizard.

### Preconditions
- User is logged in
- User has no club yet

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Land on "Create Your Club" wizard | Display club creation form |
| 2 | Enter club name (company name) | Validate uniqueness, generate slug |
| 3 | Select industry | Update form |
| 4 | Select company size | Update form |
| 5 | Upload club logo (optional) | Preview logo, validate size/format |
| 6 | Choose primary/secondary colors | Preview colors on sample card |
| 7 | Click "Create Club" | Create company record |
| 8 | - | Assign user as Club Owner (Super Admin) |
| 9 | - | Create default departments/positions (seed data) |
| 10 | - | Redirect to **Club Dashboard** |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 2a | Club name already taken | Show error "Name already in use", suggest alternatives |
| 5a | Logo > 2MB | Show error "Logo must be under 2MB" |
| 5b | Invalid format | Show error "Please upload PNG, JPG, or SVG" |

### Screens
1. Create Club Wizard (Step 1: Basic Info)
2. Create Club Wizard (Step 2: Branding)
3. Club Created Success Screen

---

## US-0.0.3: Invite Initial Squad (Scouts/Staff)

> **As a** Club Owner,  
> **I want to** invite my HR team and managers,  
> **So that** they can help me add the rest of the squad.

### Scenario
The owner invites key team members (Scouts/HR) to join the platform from the Dashboard.

### Preconditions
- Club is created
- User is logged in as Club Owner
- User is on Club Dashboard

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Click "Invite Team Members" (from Quick Actions or header) | Open invite modal |
| 2 | Enter email addresses (one-by-one or comma-separated) | Validate email format, show as tags |
| 3 | Select role for invitees (Scout/HR, Manager, etc.) | Update form |
| 4 | Add optional message | Update form |
| 5 | Click "Send Invitations" | Send invitation emails |
| 6 | - | Close modal, show success toast |
| 7 | - | Update Pending Invites section on Dashboard |
| 8 | *Invitee* clicks email link | Navigate to accept invitation page |
| 9 | *Invitee* sets password | Create user account |
| 10 | - | Redirect to Dashboard |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 2a | Email already in system | Show error "Already a member" |
| 4a | Skip invitations | Allow closing modal without sending |
| 7a | Invitation expired (7 days) | Show error "Invitation expired", prompt owner to resend |

### Screens
1. Club Dashboard (with Invite button)
2. Invite Team Modal (with email tags input)
3. Invitation Sent Toast Notification
4. Accept Invitation Page (for invitee)
5. Set Password Page (for invitee)

---

## US-0.0.4: Club Dashboard (Home)

> **As a** Club Owner,  
> **I want to** see an overview of my club's status and key metrics,  
> **So that** I can quickly understand team health and take action.

### Scenario
After creating a club or logging in, the owner lands on the Club Dashboard - the main hub for managing the team.

### Preconditions
- Club is created
- User is logged in as Club Owner or Manager

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Navigate to Dashboard | Display welcome section with greeting |
| 2 | - | Show Manager Rating circle (0-100) |
| 3 | - | Display gamification bar (Level, XP progress, Streak) |
| 4 | - | Show 4 KPI cards (Squad Size, Avg Fit, Vacancies, Dept Coverage) |
| 5 | - | Display Action Bar ("Build your team" prompt) |
| 6 | - | Show Quick Actions grid (Add Player, View Pitch, Invite, Reports) |
| 7 | - | Show Recent Activity feed |
| 8 | - | Show Pending Invites list |
| 9 | - | Show Getting Started checklist |
| 10 | Click any Quick Action | Navigate to corresponding page/modal |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 1a | No employees yet | Show "Start building your squad" prompt |
| 8a | No pending invites | Show "No pending invites, invite your team!" |
| 9a | All checklist items complete | Show "Congrats! Setup complete" badge |

### Screens
1. **Club Dashboard** (main page)

### Dashboard Components

| Component | Description |
|-----------|-------------|
| **Welcome Section** | Gradient banner with greeting, club name, manager rating circle |
| **Gamification Bar** | Level badge, XP progress bar, streak counter, achievements |
| **KPI Grid** | 4 cards: Squad Size, Average Fit Score, Vacancies ⚠️, Dept Coverage % |
| **Action Bar** | Contextual CTA ("You have 3 vacancies to fill...") |
| **Quick Actions** | 2x2 grid: Add New Player, View Formation Pitch, Invite Team, View Reports |
| **Activity Feed** | Recent actions (player added, level up, updates) |
| **Pending Invites** | List of sent invitations with status (pending/accepted) |
| **Getting Started** | Checklist: Create club ✅, Invite team, Set up positions, Add first player |

---

## Quality Checklist

- [x] All user stories from Epic 0.0 are included (4 stories)
- [x] Each story has `As a... I want to... So that...` statement
- [x] Each story has Main Flow table (Step | User Action | System Response)
- [x] Each story has Alternative Flows for error cases
- [x] Each story lists Screens involved
- [x] Flows are detailed enough for Mermaid.js conversion

---

## Related Epics

| Epic | Relation | Link |
|------|----------|------|
| **Epic 0.4** | Player Card System (includes Owner's Player Card setup) | `player-card-system.md` |
| **Epic 0.5** | Formation View (Department/Position setup) | `formation-view.md` |

---

## Output Chain

```
This PRD → UX Agent (ascendhr-ux.md)
         → Creates Mermaid.js flow diagrams
         → Feeds into v0.dev for UI generation
```
