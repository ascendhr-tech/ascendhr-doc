# Football Club Setup - User Stories

**Epic:** 0.0 - Football Club Setup (Multi-tenant)  
**Version:** 1.0  
**Created:** December 16, 2024  
**Purpose:** User stories for UX flow design

---

## User Personas

| Persona | Role | Key Actions |
|---------|------|-------------|
| **Club Owner** | CEO/Founder/Business Owner | Register account, create club, setup profile, invite team |

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
| 9 | - | Create default departments/positions |
| 10 | - | Redirect to "Setup Your Player Card" |

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

## US-0.0.3: Setup Owner's Player Card (Dogfooding)

> **As a** Club Owner,  
> **I want to** create my own Player Card,  
> **So that** I can experience the system before adding my team.

### Scenario
The owner creates their own Player Card as the first employee, experiencing the same flow they'll use for their team.

### Preconditions
- User has created their club
- User has no employee/player card yet

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | See "Set up your Player Card" prompt | Display player card setup form |
| 2 | Select position/title (CEO, Founder, etc.) | Update form |
| 3 | Select department (or create "Leadership") | Update form |
| 4 | Rate own 10 attributes using sliders | Calculate Current Ability |
| 5 | Set Potential Ability | Validate ≥ Current Ability |
| 6 | Upload profile photo (optional) | Preview photo |
| 7 | Click "Create My Player Card" | Create employee + player card |
| 8 | - | Show FM-style Player Card preview |
| 9 | - | Show "You're ready!" with next steps |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 4a | No attributes rated | Show warning "Rate at least 3 attributes" |
| 5a | Potential < Current | Show error "Potential must be ≥ Current" |

### Screens
1. Setup Player Card Prompt
2. Player Card Form (with attribute sliders)
3. Radar Chart Preview
4. Player Card Created Success (with FM-style card display)

---

## US-0.0.4: Invite Initial Squad (Scouts/Staff)

> **As a** Club Owner,  
> **I want to** invite my HR team and managers,  
> **So that** they can help me add the rest of the squad.

### Scenario
The owner invites key team members (Scouts/HR) to join the platform and help manage employees.

### Preconditions
- Club is created
- Owner has completed their player card

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Click "Invite Team Members" | Open invite modal |
| 2 | Enter email addresses (comma-separated or one-by-one) | Validate email format |
| 3 | Select role for invitees (Scout/HR, Manager, etc.) | Update form |
| 4 | Add optional message | Update form |
| 5 | Click "Send Invitations" | Send invitation emails |
| 6 | - | Show "Invitations sent" summary |
| 7 | *Invitee* clicks email link | Navigate to accept invitation page |
| 8 | *Invitee* sets password | Create user account |
| 9 | *Invitee* is prompted to create their Player Card | Start US-0.0.3 flow for invitee |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 2a | Email already in system | Show error "Already a member" |
| 4a | Skip invitations | Allow "Skip for now" option |
| 7a | Invitation expired (7 days) | Show error "Invitation expired", prompt owner to resend |

### Screens
1. Invite Team Modal
2. Invitation Sent Confirmation
3. Accept Invitation Page (for invitee)
4. Set Password Page (for invitee)

---

## Quality Checklist

- [x] All user stories from Epic 0.0 are included (4 stories)
- [x] Each story has `As a... I want to... So that...` statement
- [x] Each story has Main Flow table (Step | User Action | System Response)
- [x] Each story has Alternative Flows for error cases
- [x] Each story lists Screens involved
- [x] Flows are detailed enough for Mermaid.js conversion

---

## Output Chain

```
This PRD → UX Agent (ascendhr-ux.md)
         → Creates Mermaid.js flow diagrams
         → Feeds into v0.dev for UI generation
```
