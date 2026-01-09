# AscendHR Phase 1: Product Overview
## The Squad Planner MVP

**Document Version:** 1.0  
**Last Updated:** January 8, 2026  
**Status:** Final - Product Definition  
**Phase Duration:** 10 weeks  
**Phase Goal:** Internal Dogfooding & MVP Validation  

---

## Executive Summary

Phase 1 introduces **The Squad Planner** — a Football Manager-inspired workforce management platform that transforms employee management from administrative burden into strategic squad building.

### Phase 1 at a Glance

| Aspect | Details |
|--------|---------|
| **Product Vision** | Visual workforce management platform inspired by Football Manager |
| **Target Users** | Managers, HR Teams, Leadership |
| **Core Innovation** | Attribute-based employee profiles (1-20 ratings) + visual formation view |
| **Timeline** | 10 weeks development |
| **Deployment** | Internal dogfooding with own team |
| **Success Metric** | 100% internal team adoption + "aha moment" validation |
| **Investment** | Cost center (฿0 revenue) — 1 PO + 4 part-time devs |

### What Customers Can DO After Phase 1

✅ **Visualize entire workforce as Football Manager squad** — Formation View shows team structure with employee attributes  
✅ **Identify critical hiring gaps** — Automated gap analysis highlights weak positions and single points of failure  
✅ **Track candidates in visual pipeline** — Scouting Network Kanban board with Player Card profiles  
✅ **Make data-driven hiring decisions** — Compare candidate attributes vs squad gaps before interviews  

---

## 1. Product Vision & Strategy

### The Problem We're Solving

**Traditional HR platforms are boring, administrative, and disconnected from how managers actually think about their teams.**

**Pain Points:**
- Managers can't see team capabilities at a glance
- Skill gaps and hiring needs aren't obvious until it's too late
- Org charts show hierarchy, not actual team strengths
- Recruitment is disconnected from team composition
- Employee profiles are static resumes, not living records

### Our Solution: Football Manager for HR

Transform workforce management into an engaging, visual, strategic activity by applying Football Manager game mechanics to real-world team building.

**Core Product Philosophy:**

> **"If you can manage a championship football squad, you can manage a championship team at work."**

Instead of:
- ❌ Static employee database → ✅ Dynamic Player Card system
- ❌ Boring org chart → ✅ Visual Formation View (pitch layout)
- ❌ Spreadsheet skill tracking → ✅ 1-20 Attribute ratings
- ❌ Disconnected ATS → ✅ Scouting Network (transfer shortlist)

### Phase 1 Strategic Objectives

1. **Validate Football Manager concept** — Prove visual squad management is superior to traditional HRIS
2. **Achieve internal adoption** — Own team uses platform daily for workforce planning
3. **Demonstrate product value** — Clear "aha moments" where team sees gaps and insights they couldn't see before
4. **Build technical foundation** — API infrastructure ready for Phase 2 AI integrations
5. **Prepare for beta launch** — Product polished enough to onboard 3-5 external customers

---

## 2. Target Users & Personas

### Primary Users (Phase 1)

#### 1. Engineering/Product Managers
**Job to be Done:** Understand team capabilities, identify skill gaps, plan hiring

**Use Cases:**
- Review team composition before planning new projects
- Identify which roles need backfill vs new hires
- Compare candidate skills to squad needs
- Spot single points of failure (1 person with critical skill)

**Frequency:** Weekly check-ins, monthly planning sessions

---

#### 2. HR/People Ops Teams
**Job to be Done:** Track workforce composition, manage recruitment pipeline

**Use Cases:**
- Visualize company-wide talent distribution
- Prioritize hiring based on gap analysis
- Maintain candidate pipeline in Scouting Network
- Report on team structure to leadership

**Frequency:** Daily pipeline management, weekly reporting

---

#### 3. Leadership/Executives
**Job to be Done:** Strategic workforce planning, high-level team health visibility

**Use Cases:**
- Review formation views of key departments
- Understand hiring priorities across organization
- Compare team strengths vs business objectives
- Make informed decisions about team structure

**Frequency:** Monthly reviews, quarterly planning

---

## 3. Core Product Features

### Feature 1: 🃏 Player Card System

**What It Is:**  
Every employee gets a Football Manager-style profile with 1-20 attribute ratings across technical skills, soft skills, and potential.

**Key Attributes Categories:**
- **Technical Skills** — Coding, Design, Sales, Marketing, etc. (role-specific)
- **Mental Attributes** — Leadership, Decision Making, Teamwork, Communication
- **Physical/Operational** — Work Rate, Stamina (relevant for operational roles)
- **Potential** — Current Ability vs Potential Ability (growth trajectory)

**User Experience:**
- Clean, visual card layout (inspired by FIFA Ultimate Team)
- Color-coded ratings (Green = Strong, Yellow = Average, Red = Weak)
- Attribute history timeline (see employee growth over time)
- Quick edit mode for managers to update after 1-on-1s
- Comparison mode (compare employees or candidates side-by-side)

**Product Value:**
- **Data-driven decisions** — Hiring and team planning based on objective ratings
- **Growth tracking** — Visual evidence of employee development
- **Benchmark insights** — Compare individuals to team/company averages

**Phase 1 Scope:**
- Manual attribute entry by managers
- 10-15 pre-defined attributes per role type
- Basic attribute history (timeline view)
- Read-only for employees (manager-controlled)

---

### Feature 2: 🏟️ Formation View

**What It Is:**  
Transform boring org charts into a Football Manager pitch. See your team as a visual formation with positions representing roles.

**Visual Metaphor:**
- **Attackers (Front Line)** — Sales, Business Development, Customer-facing
- **Midfielders (Core)** — Product, Engineering, Marketing
- **Defenders (Support)** — Operations, Finance, Admin, HR
- **Goalkeeper** — Leadership/CEO

**User Experience:**
- Drag-and-drop interface to build formations
- Visual indicators: Green (strong position), Yellow (adequate), Red (gap)
- Hover over players to see mini player card
- Filter by department, team, or custom groups
- Save formation templates (e.g., "Q1 Engineering Squad")

**Product Value:**
- **Instant team visualization** — See team structure in seconds
- **Gap identification** — Red zones show hiring priorities
- **Strategic planning** — Experiment with team compositions before hiring
- **Executive presentations** — Beautiful visuals for board meetings

**Phase 1 Scope:**
- Single formation view per company/department
- Drag-and-drop player positioning
- Color-coded strength indicators
- Export as image/PDF for presentations

---

### Feature 3: 📊 Gap Analysis

**What It Is:**  
Automated detection of weak positions, missing skills, and single points of failure in your team.

**Analysis Types:**

**1. Skill Gap Analysis**
- Identifies roles where attributes fall below required threshold
- Example: "Backend Team: Database expertise below target (avg 12/20, need 16+)"

**2. Depth Analysis**
- Highlights positions with only 1 person (injury/turnover risk)
- Example: "⚠️ Warning: Only 1 Senior DevOps Engineer. High turnover risk."

**3. Succession Risk**
- Flags critical roles without backup coverage
- Example: "Critical Role: Lead Architect has no backup with >14 Technical rating"

**4. Hiring Priority Scoring**
- Ranks open positions by urgency and impact
- Factors: Gap severity, team size, business criticality

**User Experience:**
- Dashboard view with prioritized alerts
- Filter by severity (Critical, High, Medium, Low)
- Click to see detailed analysis and recommendations
- Export gap analysis report for hiring discussions

**Product Value:**
- **Proactive planning** — Spot issues before they become critical
- **Data-backed hiring** — Justify hiring requests with objective data
- **Risk mitigation** — Identify single points of failure early

**Phase 1 Scope:**
- Rule-based gap detection (no ML required)
- 3 analysis types: Skill gaps, Depth, Succession risk
- Simple alert dashboard
- Manual threshold configuration per role

---

### Feature 4: 🔍 Scouting Network (ATS-Lite)

**What It Is:**  
Lightweight applicant tracking system designed as a "Transfer Shortlist" — track candidates with Player Card profiles.

**Key Components:**

**1. Kanban Pipeline**
- Stages: Sourced → Screening → Interview → Offer → Hired
- Drag-and-drop to move candidates through stages
- Visual progress indicators

**2. Candidate Player Cards**
- Same attribute system as employees
- Current Ability (based on resume/interview)
- Potential Ability (estimated growth trajectory)
- Fit Score (% match vs position requirements)

**3. Position-Based Hiring**
- Define position requirements (e.g., "Backend Dev: Technical 16+, Teamwork 14+")
- Auto-calculate candidate fit scores
- Compare candidates to squad gaps

**4. Source Tracking**
- Track where candidates come from (LinkedIn, referral, agency, etc.)
- Measure sourcing channel effectiveness

**User Experience:**
- Clean Kanban board (inspired by Trello/Linear)
- Quick-add candidate form with attribute ratings
- Side-by-side comparison of shortlisted candidates
- One-click convert: Candidate → Employee (when hired)

**Product Value:**
- **Unified platform** — Recruitment and team management in one place
- **Data consistency** — Same attribute system for candidates and employees
- **Better hiring decisions** — Compare candidates to actual team gaps

**Phase 1 Scope:**
- Manual candidate entry (no resume parsing)
- 4-stage Kanban pipeline
- Basic fit scoring (rule-based matching)
- Position requirements configuration

---

### Feature 5: 🏗️ Multi-Tenant Club Setup

**What It Is:**  
Each customer company is a "Football Club" with branded identity and isolated data.

**Key Components:**
- Club name, logo, and brand colors
- Department/team structure (squads)
- Role position templates
- User roles (Admin, Manager, HR, Employee)

**Phase 1 Scope:**
- Single-tenant architecture (one company per instance)
- Basic branding (logo, club name)
- Department/team hierarchy
- Manager and HR admin roles

---

### Feature 6: 🔌 API Infrastructure Foundation

**What It Is:**  
REST API endpoints and webhook framework to enable Phase 2 third-party integrations.

**Key Capabilities:**
- RESTful API for core entities (employees, candidates, positions)
- Webhook receivers for external data (Phase 2: TechVue, HireVue)
- Authentication & authorization (API keys)
- Extensible data models (support for external source IDs)

**Product Value:**
- **Future-proof architecture** — Ready for AI recruitment integrations in Phase 2
- **Flexibility** — Custom integrations possible for enterprise customers

**Phase 1 Scope:**
- Basic REST API endpoints
- Webhook receiver framework (not actively used yet)
- API documentation for Phase 2 partners

---

## 5. Product Differentiation

### AscendHR vs Traditional HRIS

| Feature | Traditional HRIS | AscendHR Phase 1 |
|---------|------------------|------------------|
| **Employee Profiles** | Static resumes, job descriptions | Dynamic Player Cards with 1-20 ratings |
| **Org Visualization** | Tree diagram, boxes & lines | Formation View (football pitch metaphor) |
| **Skill Tracking** | Text fields, checkboxes | Quantified 1-20 attributes with history |
| **Gap Analysis** | Manual spreadsheet analysis | Automated detection with alerts |
| **ATS Integration** | Separate platform (Lever, Greenhouse) | Built-in Scouting Network with same data model |
| **User Experience** | Administrative, boring | Engaging, visual, game-like |

### Unique Value Propositions

**1. Football Manager UX**
- ✨ Only HRIS inspired by world-class sports management game
- ✨ Visual workforce intelligence vs traditional databases

**2. Attribute-Based Profiles**
- ✨ Quantified 1-20 ratings vs vague "proficient/expert" levels
- ✨ Comparable across employees, teams, and time periods

**3. Integrated Scouting**
- ✨ Recruitment and team management in one platform
- ✨ Compare candidates to actual squad gaps, not generic job descriptions

**4. Gap Analysis Automation**
- ✨ Proactive alerts for hiring priorities
- ✨ Data-driven insights vs manager intuition

---

## Phase 1 Deliverables

### Product Deliverables

**Core Platform:**
- ✅ Player Card System (CRUD + attribute history)
- ✅ Formation View (drag-and-drop squad builder)
- ✅ Gap Analysis (automated detection + alerts)
- ✅ Scouting Network (Kanban ATS)
- ✅ Multi-tenant Club Setup
- ✅ API Infrastructure

**User Experience:**
- ✅ Responsive web app (desktop + tablet)
- ✅ Onboarding flow for new companies
- ✅ Manager and HR admin dashboards
- ✅ Help documentation (user guides)

**Technical:**
- ✅ REST API endpoints + documentation
- ✅ Authentication & authorization
- ✅ Database schema + migrations

### Business Deliverables

- ✅ Internal case study (1-page success story)
- ✅ Beta program structure
- ✅ 3-5 beta customer commitments
- ✅ Phase 2-4 product roadmap

---