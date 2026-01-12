# AscendHR - Squad Planner MVP

**Document Version:** 3.1  
**Created:** December 2, 2024  
**Updated:** December 16, 2024  
**Status:** Planning  
**Methodology:** Lean + AI-Assisted (Vibe Coding)  
**MVP Concept:** 🎮 The Squad Planner (Football Manager-Inspired)

---

## Executive Summary

| Epic | Scope | AI-Assisted Man-days | With Buffer (20%) |
|------|-------|----------------------|-------------------|
| Epic 0.0 | Football Club Setup (Multi-tenant) | 4 | 5 |
| Epic 0.1-0.3 | Foundation + Auth | 10 | 12 |
| Epic 0.4 | Player Card System | 15 | 18 |
| Epic 0.5 | Formation View + Squad Builder | 16.5 | 20 |
| Epic 0.6 | Gap Analysis | 5 | 6 |
| Epic 0.7 | Scouting Network | 8 | 10 |
| **TOTAL** | | **58.5** | **71 man-days** |

> **AI Productivity Boost:** ~40-60% faster than traditional development

---

## 🎮 MVP Concept: "The Squad Planner"

> **Differentiation:** Instead of a boring employee database, we build a **Football Manager-inspired Squad View**.

### Core Features

| Feature | Concept | Implementation |
|---------|---------|----------------|
| **Player Card** | Every employee gets a profile with 1-20 Attributes | Technical (Coding, Sales) + Mental (Leadership, Determination) |
| **Formation View** | Visual "Pitch" instead of org chart tree | Attackers (Sales), Midfielders (Product), Defenders (Ops) |
| **Gap Analysis** | Highlights weak positions | "Warning: No depth in Customer Success. Injury risk high." |
| **Scouting Network** | Lightweight ATS as "Transfer Shortlist" | Kanban board with Current vs Potential Ability ratings |

### Dogfooding Task

1. Upload your entire team as Player Cards
2. Rate everyone 1-20 on key skills
3. Run "Squad Analysis" to find weaknesses
4. Use the data to make your next real hire

---

## Team Structure (Lean)

| Role | Count | Allocation | Weekly Hours |
|------|-------|------------|--------------|
| Full-stack Developer | 4 | Part-time (50%) | 20 hrs each |
| **Total Capacity** | | 2 FTE equivalent | 80 hrs/week |

### No Dedicated Roles Strategy
- **No UX/UI** → Use MUI components, copy proven layouts
- **No QA** → AI-generated tests, developer self-testing
- **No DevOps** → Vercel/Railway auto-deploy, simple CI/CD
- **No PM** → Developers self-organize, async coordination

---

## Timeline

| Phase | Duration | Target |
|-------|----------|--------|
| Club Setup (0.0) | 0.5 weeks | Week 0.5 |
| Foundation (0.1-0.3) | 2 weeks | Week 2.5 |
| Formation View (0.5) | 2.5 weeks | Week 5 | <!-- Enhanced with Role Templates & Squad Builder -->
| Player Cards (0.4) | 2.5 weeks | Week 7.5 | <!-- Now includes Owner's Card -->
| Gap Analysis (0.6) | 1 week | Week 8.5 |
| Scouting (0.7) | 1.5 weeks | Week 10 |
| **Total** | **~10 weeks** | **~2.5 months** |

---

## AI-Assisted Development Guidelines

### What AI Handles (40-50% of work)
- CRUD operations & forms
- Validation schemas (Yup/Zod)
- UI components & layouts
- Unit & integration tests
- API documentation
- Database migrations
- Error handling boilerplate

### What Humans Focus On
- Business logic decisions
- Architecture & security
- Code review & refinement
- Complex workflows
- Edge cases & validation rules
- Integration testing

### Workflow
```
1. Define requirement clearly
2. AI generates initial code
3. Human reviews & refines
4. AI generates tests
5. Human verifies & merges
```

# PHASE 0 - CRITICAL (Revised)

> **Total: 51 man-days (62 with buffer)**

---

## Epic 0.0: 🏟️ Football Club Setup (Multi-tenant)

**AI Boost:** High (forms, auth)  
**Estimate:** 4 man-days

> Owner-first onboarding: Create Account → Create Club → Invite Squad
> 
> ⚠️ **Note:** Player Card setup is handled in Epic 0.4 (Player Card System) since it requires Department/Position to be configured first.

### US-0.0.1: Register Account (Owner Sign Up)
| ID | Task | Est. |
|----|------|------|
| TASK-0.0.1.1 | Landing page with "Start Your Journey" CTA | 0.25d |
| TASK-0.0.1.2 | Registration form (Name, Email, Password) | 0.5d |
| TASK-0.0.1.3 | Email verification flow | 0.25d |
| TASK-0.0.1.4 | User created (no club yet - pending state) | 0.25d |

**Subtotal: 1.25 days**

### US-0.0.2: Create Your Club
| ID | Task | Est. |
|----|------|------|
| TASK-0.0.2.1 | "Create Your Club" wizard page | 0.25d |
| TASK-0.0.2.2 | Club form (name, industry, size) | 0.5d |
| TASK-0.0.2.3 | Logo upload + Club colors | 0.25d |
| TASK-0.0.2.4 | Companies table migration + multi-tenant setup | 0.5d |
| TASK-0.0.2.5 | Tenant isolation middleware | 0.5d |
| TASK-0.0.2.6 | User becomes Club Owner (Super Admin role) | 0.25d |

**Subtotal: 2.25 days**

### US-0.0.3: Invite Initial Squad (Scouts/Staff)
| ID | Task | Est. |
|----|------|------|
| TASK-0.0.3.1 | Invite team member form | 0.25d |
| TASK-0.0.3.2 | Email invitation flow | 0.25d |

**Subtotal: 0.5 days**

---

## Epic 0.1: Project Infrastructure Setup

**AI Boost:** High (boilerplate, configs)  
**Estimate:** 3 man-days

| ID | Task | Est. | AI Help |
|----|------|------|---------|
| TASK-0.1.1 | Git repo + branching strategy | 0.25d | Template |
| TASK-0.1.2 | Next.js + TypeScript + MUI + Tailwind setup | 0.5d | CLI + AI |
| TASK-0.1.3 | Prisma/Drizzle ORM setup | 0.25d | AI |
| TASK-0.1.4 | CI/CD pipeline (GitHub Actions) | 0.5d | AI template |
| TASK-0.1.5 | Docker setup | 0.5d | AI |
| TASK-0.1.6 | Environment configs | 0.25d | AI |
| TASK-0.1.7 | ESLint + Prettier config | 0.25d | AI |
| TASK-0.1.8 | Vercel/Railway deployment setup | 0.5d | AI |

---

## Epic 0.2: Core Database Design

**AI Boost:** High (migrations, schemas)  
**Estimate:** 2 man-days

| ID | Task | Est. | AI Help |
|----|------|------|---------|
| TASK-0.2.1 | ERD design for all Phase 0-1 | 0.5d | AI draft |
| TASK-0.2.2 | Users + Roles + Permissions migrations | 0.5d | AI |
| TASK-0.2.3 | Employees + Hierarchy migration | 0.25d | AI |
| TASK-0.2.4 | Departments + Positions migration | 0.25d | AI |
| TASK-0.2.5 | Consent + Audit logs migration | 0.25d | AI |
| TASK-0.2.6 | Seed data (roles, permissions) | 0.25d | AI |

---

## Epic 0.3: Authentication & Access Control

**AI Boost:** Medium (common patterns, but security critical)  
**Estimate:** 5 man-days

### US-0.3.1: User Login/Logout
| ID | Task | Est. |
|----|------|------|
| TASK-0.3.1.1 | Login form UI (MUI) | 0.25d |
| TASK-0.3.1.2 | JWT access + refresh token implementation | 0.5d |
| TASK-0.3.1.3 | Login API with rate limiting | 0.25d |
| TASK-0.3.1.4 | Logout with token invalidation | 0.25d |
| TASK-0.3.1.5 | Session persistence (remember me) | 0.25d |

**Subtotal: 1.5 days**

### US-0.3.2: Password Management
| ID | Task | Est. |
|----|------|------|
| TASK-0.3.2.1 | Password reset request form | 0.25d |
| TASK-0.3.2.2 | Reset token generation + email | 0.5d |
| TASK-0.3.2.3 | Password reset form + API | 0.5d |
| TASK-0.3.2.4 | Change password (logged in) | 0.25d |

**Subtotal: 1.5 days**

### US-0.3.3: Registration (Admin creates users)
| ID | Task | Est. |
|----|------|------|
| TASK-0.3.3.1 | Create user form (admin) | 0.25d |
| TASK-0.3.3.2 | Email invitation with temp password | 0.5d |
| TASK-0.3.3.3 | First login password change | 0.25d |

**Subtotal: 1 day**

### US-0.3.4: Auth Middleware & Guards
| ID | Task | Est. |
|----|------|------|
| TASK-0.3.4.1 | JWT verification middleware | 0.25d |
| TASK-0.3.4.2 | Role/Permission checking middleware | 0.5d |
| TASK-0.3.4.3 | Frontend auth context + hooks | 0.25d |

**Subtotal: 1 day**

---

## Epic 0.4: 🎮 Player Card System (was: Employee Database)

**AI Boost:** High (CRUD) + Medium (custom UI)  
**Estimate:** 15 man-days

> Every employee gets an FM-style Player Card with 1-20 attribute ratings
> 
> ⚠️ **Prerequisite:** Epic 0.5 Department/Position setup must be completed first, or basic Position seeding is needed.

### US-0.4.0: Setup Owner's Player Card (First Player Card)

> 🎮 **Dogfooding:** The Club Owner sets up their own Player Card as the first entry.

| ID | Task | Est. |
|----|------|------|
| TASK-0.4.0.1 | "Set up your Player Card" prompt/wizard | 0.25d |
| TASK-0.4.0.2 | Owner selects their Position/Department | 0.25d |
| TASK-0.4.0.3 | Owner rates their own 10 attributes (1-20) | 0.25d |
| TASK-0.4.0.4 | Create Employee + Player Card for Owner | 0.25d |

**Subtotal: 1 day**

### US-0.4.1: Create Employee + Player Card
| ID | Task | Est. |
|----|------|------|
| TASK-0.4.1.1 | Employee form (Formik + Yup) | 0.5d |
| TASK-0.4.1.2 | Employee ID auto-generation | 0.25d |
| TASK-0.4.1.3 | Photo upload (S3/Cloudinary) | 0.5d |
| TASK-0.4.1.4 | Create API + validation | 0.25d |
| TASK-0.4.1.5 | Auto-create user account + send invite | 0.5d |

**Subtotal: 2 days**

### US-0.4.2: Employee List & Search
| ID | Task | Est. |
|----|------|------|
| TASK-0.4.2.1 | Employee list page (MUI DataGrid) | 0.5d |
| TASK-0.4.2.2 | Search, filter, pagination API | 0.5d |
| TASK-0.4.2.3 | Filter by department, status, role | 0.25d |
| TASK-0.4.2.4 | Quick actions (view, edit, status) | 0.25d |

**Subtotal: 1.5 days**

### US-0.4.3: Employee Detail & Update (Update Attributes Wizard)
| ID | Task | Est. |
|----|------|------|
| TASK-0.4.3.1 | Employee detail page with spider chart | 0.5d |
| TASK-0.4.3.2 | Update Attributes 3-step wizard (trigger, adjust, preview) | 0.5d |
| TASK-0.4.3.3 | Update API with audit logging | 0.25d |

**Subtotal: 1.25 days**

### US-0.4.3b: Change Position/Department (Transfer Wizard)
| ID | Task | Est. |
|----|------|------|
| TASK-0.4.3b.1 | 4-step position change wizard UI | 0.5d |
| TASK-0.4.3b.2 | Fit score comparison (current vs new role) | 0.25d |
| TASK-0.4.3b.3 | Gap analysis & development recommendations | 0.25d |
| TASK-0.4.3b.4 | Position change API with history | 0.25d |

**Subtotal: 1.25 days**

### US-0.4.4: Employment Status Management
| ID | Task | Est. |
|----|------|------|
| TASK-0.4.4.1 | Status change modal | 0.25d |
| TASK-0.4.4.2 | Termination workflow | 0.25d |
| TASK-0.4.4.3 | Status history logging | 0.25d |

**Subtotal: 0.75 days**

### US-0.4.5: Reporting Structure (Hierarchy)
| ID | Task | Est. |
|----|------|------|
| TASK-0.4.5.1 | "Reports to" field in employee form | 0.25d |
| TASK-0.4.5.2 | Manager selection dropdown | 0.25d |
| TASK-0.4.5.3 | View direct reports list | 0.5d |
| TASK-0.4.5.4 | Hierarchy API (get reports, get manager chain) | 0.5d |

**Subtotal: 1.5 days**

### US-0.4.6: Bulk Import
| ID | Task | Est. |
|----|------|------|
| TASK-0.4.6.1 | CSV template download | 0.25d |
| TASK-0.4.6.2 | File upload + parsing | 0.5d |
| TASK-0.4.6.3 | Validation + bulk insert API | 0.5d |
| TASK-0.4.6.4 | Import result summary | 0.25d |

**Subtotal: 1.5 days**

### US-0.4.7: Role Assignment
| ID | Task | Est. |
|----|------|------|
| TASK-0.4.7.1 | Role assignment in employee form | 0.25d |
| TASK-0.4.7.2 | Multi-role selection | 0.25d |
| TASK-0.4.7.3 | Role assignment API | 0.25d |

**Subtotal: 0.75 days**

### US-0.4.8: 🎮 Player Card UI (NEW)
| ID | Task | Est. |
|----|------|------|
| TASK-0.4.8.1 | Player Card component (FM-style design) | 1d |
| TASK-0.4.8.2 | Attribute spider/radar chart | 0.5d |
| TASK-0.4.8.3 | Attribute rating sliders (1-20) | 0.5d |
| TASK-0.4.8.4 | Current/Potential ability calculation | 0.5d |
| TASK-0.4.8.5 | Player comparison modal (side-by-side) | 0.75d |
| TASK-0.4.8.6 | Attribute history tracking | 0.5d |
| TASK-0.4.8.7 | Player Card gallery view | 0.25d |

**Subtotal: 4 days**

---

## Epic 0.5: ⚽ Formation View + Squad Builder

**AI Boost:** Medium (custom visualization + role configuration)  
**Estimate:** 16.5 man-days

> Visual "Pitch" view with deep role/attribute configuration - the organizational backbone

### US-0.5.1: Department Management
| ID | Task | Est. |
|----|------|------|
| TASK-0.5.1.1 | Department list page | 0.25d |
| TASK-0.5.1.2 | Create/edit department modal | 0.5d |
| TASK-0.5.1.3 | Zone assignment (Attack/Midfield/Defense/Support) | 0.5d |
| TASK-0.5.1.4 | Zone visual preview | 0.25d |
| TASK-0.5.1.5 | Department CRUD APIs | 0.25d |

**Subtotal: 1.75 days**

### US-0.5.2: Position/Role Management (Enhanced)
| ID | Task | Est. |
|----|------|------|
| TASK-0.5.2.1 | Position list (grouped by zone) | 0.25d |
| TASK-0.5.2.2 | Create/edit position modal | 0.5d |
| TASK-0.5.2.3 | Pitch position (x,y coordinates) | 0.5d |
| TASK-0.5.2.4 | Attribute requirements configuration | 0.75d |
| TASK-0.5.2.5 | Apply role template to position | 0.25d |
| TASK-0.5.2.6 | Position CRUD APIs | 0.25d |

**Subtotal: 2.5 days**

### US-0.5.3: 🎯 Attribute Configuration System (NEW)
| ID | Task | Est. |
|----|------|------|
| TASK-0.5.3.1 | Attribute definitions management UI | 0.5d |
| TASK-0.5.3.2 | Core vs Specialist attribute categorization | 0.25d |
| TASK-0.5.3.3 | Zone-based attribute filtering | 0.25d |
| TASK-0.5.3.4 | Importance levels (Critical/Important/Nice-to-have) | 0.25d |
| TASK-0.5.3.5 | Role card preview with configured attributes | 0.5d |
| TASK-0.5.3.6 | Attribute definitions API | 0.25d |
| TASK-0.5.3.7 | 🗑️ Delete attribute with confirmation modal | 0.25d |

**Subtotal: 2.25 days**

### US-0.5.4: 📋 Role Templates Library (NEW)
| ID | Task | Est. |
|----|------|------|
| TASK-0.5.4.1 | Role templates gallery view | 0.5d |
| TASK-0.5.4.2 | Template preview card | 0.25d |
| TASK-0.5.4.3 | Apply template to position | 0.25d |
| TASK-0.5.4.4 | Create custom template from position | 0.25d |
| TASK-0.5.4.5 | Role templates CRUD API | 0.25d |

**Subtotal: 1.5 days**

### US-0.5.5: 🏟️ Formation / Pitch View
| ID | Task | Est. |
|----|------|------|
| TASK-0.5.5.1 | Pitch canvas component (SVG/Canvas) | 1.5d |
| TASK-0.5.5.2 | Drag-and-drop player positioning | 1d |
| TASK-0.5.5.3 | Department zone overlays | 0.5d |
| TASK-0.5.5.4 | Player card tooltips with fit score | 0.5d |
| TASK-0.5.5.5 | Zoom/Pan controls | 0.5d |
| TASK-0.5.5.6 | Formation template system | 0.5d |
| TASK-0.5.5.7 | Export formation as image | 0.25d |
| TASK-0.5.5.8 | Mobile-responsive pitch view | 0.5d |
| TASK-0.5.5.9 | Formation data API | 0.5d |
| TASK-0.5.5.10 | 🗑️ Delete position from formation | 0.25d |

**Subtotal: 6 days**

### US-0.5.6: 🎮 Squad Builder (Enhanced)
| ID | Task | Est. |
|----|------|------|
| TASK-0.5.6.1 | Squad template selection/creation | 0.5d |
| TASK-0.5.6.2 | Squad template slots configuration | 0.25d |
| TASK-0.5.6.3 | Squad builder canvas (formation view) | 0.5d |
| TASK-0.5.6.4 | Player selection panel | 0.25d |
| TASK-0.5.6.5 | Drag player to position slot | 0.25d |
| TASK-0.5.6.6 | Real-time fit score calculation | 0.5d |
| TASK-0.5.6.7 | Best-fit player suggestions | 0.25d |
| TASK-0.5.6.8 | Squad health overview (filled vs empty slots) | 0.25d |
| TASK-0.5.6.9 | Squad CRUD APIs | 0.25d |
| TASK-0.5.6.10 | 🗑️ Delete squad with confirmation modal | 0.25d |
| TASK-0.5.6.11 | 🗑️ Remove player from squad slot | 0.25d |

**Subtotal: 3.5 days**

---

## Epic 0.6: 🎯 Gap Analysis System

**AI Boost:** Medium (algorithm complexity)  
**Estimate:** 5 man-days

> Automatically identify weak positions in your squad - the killer feature

### US-0.6.1: Position Requirements
| ID | Task | Est. |
|----|------|------|
| TASK-0.6.1.1 | Position requirement configuration UI | 0.5d |
| TASK-0.6.1.2 | Set min/ideal headcount per position | 0.25d |
| TASK-0.6.1.3 | Define critical attributes per position | 0.5d |
| TASK-0.6.1.4 | Position requirements CRUD API | 0.25d |

**Subtotal: 1.5 days**

### US-0.6.2: Gap Analysis Engine
| ID | Task | Est. |
|----|------|------|
| TASK-0.6.2.1 | Gap detection algorithm | 1d |
| TASK-0.6.2.2 | "Injury risk" calculation (single point of failure) | 0.5d |
| TASK-0.6.2.3 | Position depth chart view | 0.5d |
| TASK-0.6.2.4 | Gap analysis API | 0.25d |

**Subtotal: 2.25 days**

### US-0.6.3: Gap Analysis Dashboard
| ID | Task | Est. |
|----|------|------|
| TASK-0.6.3.1 | Squad health score widget | 0.5d |
| TASK-0.6.3.2 | Weakness warning banners | 0.25d |
| TASK-0.6.3.3 | Recommended hire profiles | 0.25d |
| TASK-0.6.3.4 | Gap analysis report PDF | 0.25d |

**Subtotal: 1.25 days**

---

## Epic 0.7: ⚽ Scouting Network (Lightweight ATS)

**AI Boost:** High (CRUD, Kanban)  
**Estimate:** 8 man-days

> Simple but engaging candidate tracking - "Transfer Shortlist" instead of boring ATS

### US-0.7.1: Scouted Player Management
| ID | Task | Est. |
|----|------|------|
| TASK-0.7.1.1 | Add scouted player form | 0.5d |
| TASK-0.7.1.2 | Scouted player card (mini player card style) | 0.75d |
| TASK-0.7.1.3 | Current vs Potential ability sliders | 0.5d |
| TASK-0.7.1.4 | Attribute rating input | 0.5d |
| TASK-0.7.1.5 | Scouted players CRUD API | 0.5d |

**Subtotal: 2.75 days**

### US-0.7.2: Scouting Kanban Board
| ID | Task | Est. |
|----|------|------|
| TASK-0.7.2.1 | Kanban board UI (Scouted → Contacted → Interviewing → Offer → Hired) | 1.5d |
| TASK-0.7.2.2 | Drag-drop status changes | 0.5d |
| TASK-0.7.2.3 | Quick view card on hover | 0.25d |
| TASK-0.7.2.4 | Pipeline status API | 0.25d |

**Subtotal: 2.5 days**

### US-0.7.3: Scouting Activities
| ID | Task | Est. |
|----|------|------|
| TASK-0.7.3.1 | Activity log per candidate | 0.5d |
| TASK-0.7.3.2 | Interview notes | 0.25d |
| TASK-0.7.3.3 | Compare scouted player vs team average | 0.75d |

**Subtotal: 1.5 days**

### US-0.7.4: Convert & Import
| ID | Task | Est. |
|----|------|------|
| TASK-0.7.4.1 | Convert scouted player to employee | 0.5d |
| TASK-0.7.4.2 | Bulk import from CSV | 0.5d |
| TASK-0.7.4.3 | LinkedIn URL scraping (basic) | 0.25d |

**Subtotal: 1.25 days**

---

# Weekly Sprint Plan

| Week | Focus | Dev 1-2 | Dev 3-4 |
|------|-------|---------|---------|
| **1** | Club Setup + Foundation | Club Registration (0.0) + Infrastructure (0.1) | Database + Auth (0.2, 0.3) |
| **2** | Auth Complete | Auth complete (0.3) | Auth testing + Security review |
| **3** | Formation View | Department/Position setup (0.5) | Attribute Config (0.5) |
| **4** | Formation View | Role Templates (0.5.4) | Pitch View (0.5.5) |
| **5** | Formation + Player Cards | Squad Builder (0.5.6) | Owner Player Card (0.4) |
| **6** | Player Cards | Player Card DB + UI (0.4) | Attributes + Ability (0.4) |
| **7** | Player Cards | Player comparison + Hierarchy (0.4) | Bulk import (0.4) |
| **8** | Gap Analysis | Gap algorithm (0.6) | Gap Dashboard (0.6) |
| **9** | Scouting Network | Scouted players (0.7) | Kanban board (0.7) |
| **10** | Scouting + Polish | Scouting features (0.7) | Bug fixes, testing, deployment |

---

# Lean Development Practices

## 1. AI-First Workflow
```
Morning: Review AI-generated code from overnight
Midday: Focus sessions on complex logic
Evening: Queue AI tasks for overnight generation
```

## 2. Part-Time Coordination
- **Async standup:** Daily text update by 10am
- **Sync call:** Weekly 30min (start of week)
- **Task ownership:** 1 person per story
- **Handoff notes:** Required for in-progress work

## 3. No UX/UI Shortcuts
- Use MUI default theme (customize colors only)
- Copy layout patterns from MUI templates
- Functional > Beautiful (but FM-inspired aesthetic!)
- Iterate on UI post-MVP

## 4. Testing Strategy (No QA)
- AI generates unit tests (80% target)
- Developer tests own features
- Critical path E2E tests only
- TypeScript strict mode = safety net

## 5. Definition of Done (Lean)
- [ ] Code merged to develop
- [ ] TypeScript compiles (no errors)
- [ ] Basic tests pass
- [ ] Works on desktop + mobile
- [ ] API auto-documented

---

# Risk Mitigation

| Risk | Strategy |
|------|----------|
| Part-time coordination | Clear ownership, async-first |
| AI generates bugs | All AI code reviewed by human |
| Scope creep | Strict MVP mindset - Squad Planner ONLY |
| Complex pitch visualization | Use existing canvas/SVG libs |
| No QA | TypeScript + AI tests + strict PR review |

---

# Summary

| Metric | Value |
|--------|-------|
| Total Epics | 8 |
| Total User Stories | ~30 |
| Total Man-days | 58.5 (71 with buffer) |
| Team Size | 4 part-time (2 FTE) |
| Timeline | **~10 weeks (~2.5 months)** |
| Target Industry | **Software House / Digital Agency** |
| AI Productivity Gain | ~40-50% |
| Key Innovation | **FM-Style Squad Planning + Squad Templates** |

---

# Next Steps

1. ☐ Finalize tech stack decisions
2. ☐ Setup project repository
3. ☐ Create Jira project with epics
4. ☐ Import user stories
5. ☐ **Dogfooding:** Upload team, rate 1-20, run Squad Analysis
6. ☐ Begin Sprint 1

