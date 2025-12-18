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

> **AI Productivity Boost:** ~40-50% faster than traditional development

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

---

# FLEXIBLE ROLE & HIERARCHY SYSTEM

> **Key Change:** Instead of hardcoded Admin/Employee, build a scalable permission system that supports any organizational structure.

## Database Schema

### �️ Company (Football Club) Schema

```sql
-- Companies (Multi-tenant clubs)
companies (
  id: UUID PRIMARY KEY,
  name: VARCHAR(200) NOT NULL,           -- 'Manchester United FC'
  slug: VARCHAR(100) UNIQUE,              -- 'manchester-united'
  industry: VARCHAR(100),                 -- 'Technology', 'Finance', etc.
  size: VARCHAR(50),                      -- 'startup', 'small', 'medium', 'enterprise'
  logo_url: VARCHAR(500),
  primary_color: VARCHAR(7),              -- '#DA291C'
  secondary_color: VARCHAR(7),            -- '#FFE500'
  
  -- Club Settings
  timezone: VARCHAR(50) DEFAULT 'Asia/Bangkok',
  date_format: VARCHAR(20) DEFAULT 'DD/MM/YYYY',
  formation_type: VARCHAR(50) DEFAULT '4-3-3',
  
  -- Status
  status: VARCHAR(50) DEFAULT 'active',   -- 'trial', 'active', 'suspended'
  trial_ends_at: TIMESTAMP,
  
  -- Onboarding
  onboarding_completed: BOOLEAN DEFAULT false,
  
  created_by: UUID REFERENCES users(id),
  created_at: TIMESTAMP,
  updated_at: TIMESTAMP
)

-- Add company_id to all tables for multi-tenancy
-- employees.company_id, users.company_id, departments.company_id, etc.
```

### 🎮 Squad Planner Schemas

```sql
-- Attribute Definitions (Master list of all attributes)
attribute_definitions (
  id: UUID PRIMARY KEY,
  name: VARCHAR(100) NOT NULL,           -- 'Coding', 'Leadership', 'Negotiation'
  code: VARCHAR(50) NOT NULL UNIQUE,     -- 'coding', 'leadership', 'negotiation'
  category: VARCHAR(20) NOT NULL,        -- 'core' or 'specialist'
  zone: VARCHAR(20),                     -- 'attack', 'midfield', 'defense', 'support' (NULL for core)
  icon: VARCHAR(50),                     -- emoji or icon name
  description: TEXT,
  is_active: BOOLEAN DEFAULT true,
  display_order: INTEGER,
  created_at: TIMESTAMP
)

-- Role Templates (Pre-configured common roles)
role_templates (
  id: UUID PRIMARY KEY,
  name: VARCHAR(100) NOT NULL,           -- 'Software Developer'
  code: VARCHAR(50) NOT NULL UNIQUE,     -- 'software_developer'
  zone: VARCHAR(20) NOT NULL,            -- 'midfield'
  department_type: VARCHAR(50),          -- 'Engineering'
  description: TEXT,
  icon: VARCHAR(50),
  color: VARCHAR(7),
  attribute_config: JSONB NOT NULL,      -- Pre-configured attribute requirements
  is_system: BOOLEAN DEFAULT false,      -- System templates can't be deleted
  company_id: UUID,                      -- NULL for system templates
  created_at: TIMESTAMP
)

-- Role Attribute Requirements (Which attributes matter per position)
role_attribute_requirements (
  id: UUID PRIMARY KEY,
  position_id: UUID REFERENCES positions(id),
  attribute_id: UUID REFERENCES attribute_definitions(id),
  importance: VARCHAR(20) NOT NULL,      -- 'critical', 'important', 'nice-to-have'
  min_value: INTEGER CHECK (min_value BETWEEN 1 AND 20),
  ideal_value: INTEGER CHECK (ideal_value BETWEEN 1 AND 20),
  weight: DECIMAL(3,2) DEFAULT 1.00,     -- For fit score calculation
  UNIQUE(position_id, attribute_id)
)

-- Employee Attributes (FM-Style 1-20 ratings - Flexible JSONB)
employee_attributes (
  id: UUID PRIMARY KEY,
  employee_id: UUID REFERENCES employees(id),
  
  -- Flexible attribute storage (allows any attributes)
  core_attributes: JSONB NOT NULL,       -- {"leadership": 15, "teamwork": 12, "communication": 14, ...}
  specialist_attributes: JSONB NOT NULL, -- {"coding": 18, "problem_solving": 16, ...}
  
  -- Calculated Ability Scores
  current_ability: INTEGER CHECK (current_ability BETWEEN 1 AND 200),
  potential_ability: INTEGER CHECK (potential_ability BETWEEN 1 AND 200),
  
  last_assessed_at: TIMESTAMP,
  assessed_by: UUID REFERENCES users(id),
  created_at: TIMESTAMP,
  updated_at: TIMESTAMP
)

-- Position Roles (Attack/Midfield/Defense mapping)
position_roles (
  id: UUID PRIMARY KEY,
  name: VARCHAR(50) NOT NULL,            -- 'Striker', 'Midfielder', 'Defender'
  zone: VARCHAR(20) NOT NULL,            -- 'attack', 'midfield', 'defense', 'support'
  department_type: VARCHAR(50),          -- Maps to: 'Sales', 'Product', 'Operations'
  template_id: UUID REFERENCES role_templates(id), -- Link to role template
  color: VARCHAR(7),
  pitch_position_x: INTEGER,             -- X coordinate (0-100)
  pitch_position_y: INTEGER              -- Y coordinate (0-100)
)

-- Formation Templates
formations (
  id: UUID PRIMARY KEY,
  name: VARCHAR(100) NOT NULL,           -- '4-3-3', '4-4-2 Diamond'
  layout_config: JSONB,
  is_default: BOOLEAN DEFAULT false,
  company_id: UUID,
  created_at: TIMESTAMP
)

-- Position Requirements (for Gap Analysis)
position_requirements (
  id: UUID PRIMARY KEY,
  position_id: UUID REFERENCES positions(id),
  min_headcount: INTEGER DEFAULT 1,
  ideal_headcount: INTEGER DEFAULT 1,
  critical_attributes: JSONB,            -- {"coding": 15, "leadership": 12}
  created_at: TIMESTAMP
)

-- Scouted Players (Lightweight ATS)
scouted_players (
  id: UUID PRIMARY KEY,
  name: VARCHAR(200) NOT NULL,
  email: VARCHAR(255),
  linkedin_url: VARCHAR(500),
  resume_url: VARCHAR(500),
  photo_url: VARCHAR(500),
  
  target_position_id: UUID REFERENCES positions(id),
  
  -- Ability Ratings
  current_ability: INTEGER CHECK (current_ability BETWEEN 1 AND 200),
  potential_ability: INTEGER CHECK (potential_ability BETWEEN 1 AND 200),
  attributes: JSONB,
  
  -- Pipeline  
  status: VARCHAR(50) DEFAULT 'scouted', -- scouted, contacted, interviewing, offer, hired
  source: VARCHAR(100),                  -- 'linkedin', 'referral'
  scout_notes: TEXT,
  scouted_by: UUID REFERENCES users(id),
  created_at: TIMESTAMP
)

-- Squad Templates (Define team structure)
squad_templates (
  id: UUID PRIMARY KEY,
  name: VARCHAR(100) NOT NULL,           -- 'Scrum Team', 'Design Team'
  description: TEXT,
  icon: VARCHAR(50),
  is_system: BOOLEAN DEFAULT false,      -- System templates can't be deleted
  company_id: UUID,                      -- NULL for system templates
  created_at: TIMESTAMP
)

-- Squad Template Slots (Positions in a squad template)
squad_template_slots (
  id: UUID PRIMARY KEY,
  template_id: UUID REFERENCES squad_templates(id),
  position_id: UUID REFERENCES positions(id),
  min_count: INTEGER DEFAULT 1,          -- Minimum players for this position
  max_count: INTEGER DEFAULT 1,          -- Maximum players for this position
  is_required: BOOLEAN DEFAULT true,     -- Required or optional slot
  display_order: INTEGER                 -- Order in formation view
)

-- Squads (Actual teams)
squads (
  id: UUID PRIMARY KEY,
  name: VARCHAR(100) NOT NULL,           -- 'Alpha Team', 'Phoenix Squad'
  template_id: UUID REFERENCES squad_templates(id),
  company_id: UUID REFERENCES companies(id),
  status: VARCHAR(20) DEFAULT 'active',  -- 'active', 'archived'
  created_at: TIMESTAMP,
  updated_at: TIMESTAMP
)

-- Squad Members (Player assignments to squads)
squad_members (
  id: UUID PRIMARY KEY,
  squad_id: UUID REFERENCES squads(id),
  employee_id: UUID REFERENCES employees(id),
  position_id: UUID REFERENCES positions(id),
  assigned_at: TIMESTAMP,
  assigned_by: UUID REFERENCES users(id),
  UNIQUE(squad_id, employee_id)          -- Each player in one position per squad
)
```

### Pre-seeded Attributes (Software House Focus)

> 🏢 **Target Industry:** Software House / Digital Agency

**Core Attributes (5)** - Apply to ALL roles:
| Attribute | Code | Description |
|-----------|------|-------------|
| Leadership | `leadership` | Leading teams and projects |
| Teamwork | `teamwork` | Agile collaboration |
| Communication | `communication` | With team and clients |
| Adaptability | `adaptability` | Tech changes fast |
| Determination | `determination` | Meeting deadlines |

**Specialist Attributes (15)** - Role-specific:
| Category | Attributes | Description |
|----------|------------|-------------|
| **Engineering** | `coding` | Programming and development skills |
| | `system_design` | Architecture and scalability thinking |
| | `problem_solving` | Debugging and finding solutions |
| | `code_quality` | Clean, maintainable, tested code |
| | `technical_learning` | Staying current with new tech |
| **Design** | `visual_design` | Aesthetics and UI skills |
| | `ux_thinking` | User-centered design approach |
| | `prototyping` | Wireframes and mockups |
| **Business** | `client_relations` | Managing client expectations |
| | `negotiation` | Contract and rate negotiation |
| | `presentation` | Pitching and demos |
| | `upselling` | Expanding existing accounts |
| **Operations** | `process_management` | Workflows and SOPs |
| | `documentation` | Record keeping and specs |
| | `talent_acquisition` | Recruiting tech talent |

### Pre-seeded Role Templates (10 - Software House)

| # | Role | Zone | Department | Key Attributes (min/ideal) |
|---|------|------|------------|---------------------------|
| 1 | **Frontend Developer** | Midfield | Engineering | Coding 14/17, Visual Design 11/14, Problem Solving 13/16 |
| 2 | **Backend Developer** | Midfield | Engineering | Coding 15/18, System Design 13/16, Problem Solving 14/17 |
| 3 | **Full-stack Developer** | Midfield | Engineering | Coding 14/17, System Design 12/15, Technical Learning 13/16 |
| 4 | **UX/UI Designer** | Midfield | Design | UX Thinking 15/18, Visual Design 14/17, Prototyping 13/16 |
| 5 | **Product Manager** | Midfield | Product | Communication 15/17, Problem Solving 13/16, Leadership 12/15 |
| 6 | **QA Engineer** | Midfield | Engineering | Code Quality 14/17, Problem Solving 13/16, Documentation 12/15 |
| 7 | **DevOps Engineer** | Midfield | Engineering | System Design 14/17, Technical Learning 13/16, Process Management 12/15 |
| 8 | **Tech Lead** | Midfield | Engineering | Leadership 14/17, Coding 13/16, Communication 13/16 |
| 9 | **Account Manager** | Attack | Sales | Client Relations 15/18, Communication 14/16, Upselling 12/15 |
| 10 | **HR / Recruiter** | Support | HR | Talent Acquisition 14/17, Communication 14/16, Process Management 11/14 |

### Pre-seeded Squad Templates (4 - Software House)

> 🏈 **Squad = Cross-functional team** (like a football squad with specific positions)

| # | Squad Template | Positions | Min-Max | Description |
|---|---------------|-----------|---------|-------------|
| 1 | **Scrum Team** | Product Manager | 1 | Classic agile team |
| | | UX/UI Designer | 1-2 | |
| | | Developer (any) | 2-5 | |
| | | QA Engineer | 1 | |
| 2 | **Full-stack Team** | Tech Lead | 1 | Small delivery team |
| | | Full-stack Developer | 2-4 | |
| | | QA Engineer | 0-1 | Optional |
| 3 | **Design Team** | Product Manager | 1 | Design-focused team |
| | | UX/UI Designer | 2-4 | |
| | | Frontend Developer | 1-2 | For prototypes |
| 4 | **DevOps Team** | DevOps Engineer | 2-4 | Infrastructure team |
| | | Backend Developer | 1-2 | |
| | | QA Engineer | 0-1 | Optional |

### Core System Schemas

```sql
-- Roles (Dynamic, Admin-configurable)
roles (
  id: UUID PRIMARY KEY,
  name: VARCHAR(100) NOT NULL UNIQUE,
  level: INTEGER NOT NULL,  -- 0=highest (Super Admin), 99=lowest
  description: TEXT,
  is_system_role: BOOLEAN DEFAULT false,
  is_active: BOOLEAN DEFAULT true,
  created_at: TIMESTAMP
)

-- Permissions (Granular actions)
permissions (
  id: UUID PRIMARY KEY,
  resource: VARCHAR(50) NOT NULL,  -- 'employee', 'leave', 'announcement'
  action: VARCHAR(50) NOT NULL,    -- 'create', 'read', 'update', 'delete', 'approve'
  description: TEXT,
  UNIQUE(resource, action)
)

-- Role-Permission Mapping
role_permissions (
  id: UUID PRIMARY KEY,
  role_id: UUID REFERENCES roles(id),
  permission_id: UUID REFERENCES permissions(id),
  UNIQUE(role_id, permission_id)
)

-- User-Role Assignment (can have multiple roles)
user_roles (
  id: UUID PRIMARY KEY,
  user_id: UUID REFERENCES users(id),
  role_id: UUID REFERENCES roles(id),
  assigned_at: TIMESTAMP,
  assigned_by: UUID REFERENCES users(id),
  UNIQUE(user_id, role_id)
)

-- Employee Hierarchy (Reporting Structure)
employee_hierarchy (
  id: UUID PRIMARY KEY,
  employee_id: UUID REFERENCES employees(id) UNIQUE,
  reports_to_id: UUID REFERENCES employees(id),
  effective_date: DATE NOT NULL,
  created_at: TIMESTAMP
)
```

## Pre-seeded System Roles

| Role | Level | Permissions | Use Case |
|------|-------|-------------|----------|
| Super Admin | 0 | All permissions | System owner, IT |
| HR Admin | 1 | All HR operations | HR department head |
| HR Staff | 2 | Employee management, leave management | HR team members |
| Department Head | 3 | View department, approve leaves | Directors, Heads |
| Manager | 4 | View team, approve team leaves | Team managers |
| Team Lead | 5 | View team members | Project leads |
| Employee | 10 | Self-service only | All employees |

## Pre-seeded Permissions

| Resource | Actions |
|----------|---------|
| `employee` | create, read, read_all, update, update_all, delete, import |
| `department` | create, read, update, delete |
| `position` | create, read, update, delete |
| `leave_type` | create, read, update, delete |
| `leave_request` | create, read, read_all, approve, reject, cancel |
| `leave_balance` | read, read_all, adjust |
| `announcement` | create, read, update, delete, publish |
| `report` | generate, export |
| `role` | create, read, update, delete, assign |
| `settings` | read, update |

## Hierarchy-Aware Features

### Leave Approval Flow
```
Employee submits leave
    ↓
System finds reports_to (Manager)
    ↓
Manager receives approval request
    ↓
If Manager unavailable → escalate to Manager's reports_to
    ↓
Approved/Rejected → notify Employee
```

### Data Visibility Rules
- **Employee:** See only own data
- **Manager:** See direct reports' data
- **Department Head:** See department data
- **HR Staff:** See all employee data
- **Super Admin:** See everything including audit logs

---

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

### US-0.4.3: Employee Detail & Update
| ID | Task | Est. |
|----|------|------|
| TASK-0.4.3.1 | Employee detail page | 0.5d |
| TASK-0.4.3.2 | Edit employee form | 0.25d |
| TASK-0.4.3.3 | Update API with audit logging | 0.25d |

**Subtotal: 1 day**

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

**Subtotal: 2 days**

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

**Subtotal: 5.75 days**

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

**Subtotal: 3 days**

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

