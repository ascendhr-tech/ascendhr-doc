# AscendHR Design Tasks & Success Roadmap

**Document Purpose:** Jira-ready task list for Design Team aligned with AscendHR Business Milestones & Success Roadmap  
**Target Audience:** Design Team, UX/UI Designers, Product Owner  
**Jira Board:** Design Team  
**Last Updated:** January 9, 2026  

---

## 📋 Overview

This document provides actionable design tasks mapped directly to the **4-phase milestone roadmap**. Each task is designed to be imported into Jira with clear deliverables, priorities, and success criteria.

**Phase Structure:**
- **Phase 1:** Internal Dogfooding (10 weeks) - MVP Design
- **Phase 2:** AI Recruitment & Evaluation (6-8 weeks + 4 weeks GTM) - Beta Testing Design
- **Phase 3:** Social + Progress Engine (8-10 weeks + 12 weeks GTM) - Market Launch Design
- **Phase 4:** Predictive Alerts Engine (8-10 weeks) - Executive Features Design

**Priority Levels:**
- **P0 (Critical)** - Must complete for phase success (blocks development or launch)
- **P1 (High)** - Important for achieving phase goals and quality
- **P2 (Medium)** - Nice to have, can defer if needed

**Design Tools & Workflow:**
- **HTML Prototypes** (`ascendhr/design/`) - Interactive mockups using shared CSS
- **Mermaid Diagrams** (`ascendhr/ux/`) - UX flow documentation (.mmd files)
- **AI Agents** (`.agent/rules/`) - Automated design assistance:
  - `ascendhr-ui-designer.md` - Generates interactive HTML mockups
  - `ascendhr-ux.md` - Creates comprehensive Mermaid UX flows
- **Design System** (`ascendhr/design/design-system.md`) - Source of truth for styles
- **Shared CSS** (`ascendhr/design/_shared/base.css`) - Unified component library
- Figma (optional - for complex visual design)
- Adobe Illustrator (branding, icons)
- Loom/ScreenFlow (video tutorials)

---

## 🎨 Design Workflow Overview

**AscendHR uses a code-based, AI-assisted design workflow:**

### 1. UX Documentation (`ascendhr/ux/`)
- Create Mermaid diagrams (.mmd files) for ALL user flows
- Cover all 10 flow types: happy path, errors, recovery, loops, timeouts, etc.
- Store in `ascendhr/ux/{feature}/` with README index
- **AI Agent:** `.agent/rules/ascendhr-ux.md` generates comprehensive flows

### 2. Interactive HTML Prototypes (`ascendhr/design/`)
- Generate interactive HTML mockups from Mermaid flows
- Use shared CSS: `ascendhr/design/_shared/base.css`
- Store in `ascendhr/design/{feature}/` with README index
- **AI Agent:** `.agent/rules/ascendhr-ui-designer.md` converts flows → HTML

### 3. Design System (`ascendhr/design/design-system.md`)
- Source of truth for colors, typography, components
- CSS variables in `base.css` define all design tokens
- Component library documented with HTML examples

### 4. Developer Handoff
- Developers use HTML prototypes as reference
- Copy CSS components from `base.css` to React/Next.js
- Mermaid flows document all edge cases and states

**Benefits:**
- ✅ Version-controlled design (Git)
- ✅ AI agents accelerate design creation
- ✅ Interactive prototypes (not static images)
- ✅ Developers understand implementation easily
- ✅ All edge cases documented in Mermaid

---

## Phase 1: 🎮 Internal Dogfooding (Weeks 1-10)

**Goal:** Design and validate MVP internally, prove Football Manager concept works

**Design Milestones:**
- MVP UI/UX designed and validated
- Core Football Manager concept proven through design
- Design system foundation established

---

### UX Research & Strategy

- [ ] **[P0] Competitive UX Analysis** - Analyze 8+ HRIS platforms (BambooHR, Workday, ChartHop)  
  *Timeline:* Week 1-2  
  *Deliverable:* UX analysis report (Markdown) with screenshots, feature comparison, pain points  
  *Success Criteria:* Clear differentiation opportunities identified  
  *AI Assist:* Use `.agent/rules/ascendhr-ux.md` for analysis framework

- [ ] **[P0] Internal User Research** - Interview internal team about workforce management needs  
  *Timeline:* Week 1-2  
  *Deliverable:* Research findings doc with user quotes, pain points, opportunities  
  *Success Criteria:* 10+ actionable insights captured

- [ ] **[P0] Information Architecture** - Define IA for entire Squad Planner platform  
  *Timeline:* Week 1-3  
  *Deliverable:* Site map Mermaid diagram (`ascendhr/ux/00-site-map.mmd`)  
  *Success Criteria:* All Phase 1 features mapped, logical grouping validated  
  *AI Assist:* Use `.agent/rules/ascendhr-ux.md` for site map structure

- [ ] **[P0] Core User Flows** - Map key user journeys (Manager reviews team, HR adds candidate)  
  *Timeline:* Week 2-3  
  *Deliverable:* Mermaid flow diagrams (.mmd files) covering all 10 flow types (happy, error, recovery, etc.) in `ascendhr/ux/{feature}/`  
  *Success Criteria:* Flows complete in <5 steps, no dead ends, all edge cases covered  
  *AI Assist:* Use `.agent/rules/ascendhr-ux.md` for comprehensive flow coverage

- [ ] **[P1] User Personas** - Create detailed personas (Manager, HR, Leadership)  
  *Timeline:* Week 2-3  
  *Deliverable:* 3 persona documents with goals, pain points, behaviors  
  *Success Criteria:* Used in design critiques and decision making

- [ ] **[P2] Jobs-to-be-Done Framework** - Define JTBD for each user type  
  *Timeline:* Week 3-4  
  *Deliverable:* JTBD map with user goals and desired outcomes  
  *Success Criteria:* Validates feature prioritization

---

### UI Design - Core Features

- [ ] **[P0] Player Card System Design** - Design employee profile cards with 1-20 attributes  
  *Timeline:* Week 2-4  
  *Deliverable:* Interactive HTML prototypes in `ascendhr/design/player-card-system/` (view, edit, compare modes)  
  *Success Criteria:* Attributes clearly visible, ratings intuitive, mobile-ready, clickable interactions  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` to generate HTML mockups from UX flows

- [ ] **[P0] Formation View Design** - Design visual "pitch" layout with drag-drop  
  *Timeline:* Week 3-5  
  *Deliverable:* Interactive HTML prototype in `ascendhr/design/formation-view/` with working drag-drop  
  *Success Criteria:* "Aha moment" achieved in 30 seconds, gaps obvious, drag-drop functional  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` + shared CSS from `base.css`

- [ ] **[P0] Gap Analysis Dashboard** - Design automated gap detection interface  
  *Timeline:* Week 4-6  
  *Deliverable:* Interactive HTML dashboard in `ascendhr/design/gap-analysis/` with alerts, filters, detail views  
  *Success Criteria:* Critical gaps visible in 10 seconds, actionable recommendations, interactive filtering  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` for dashboard components

- [ ] **[P0] Scouting Network Kanban** - Design ATS-lite with candidate pipeline  
  *Timeline:* Week 5-7  
  *Deliverable:* Interactive HTML Kanban in `ascendhr/design/scouting-network/` with drag-drop  
  *Success Criteria:* Add candidate <5 min, drag-drop smooth, fit scores clear, state management working  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` for Kanban interactions

- [ ] **[P0] Squad Builder Interface** - Design drag-drop team formation builder  
  *Timeline:* Week 4-6  
  *Deliverable:* Interactive HTML prototype in `ascendhr/design/squad-builder/` with drag-drop JavaScript  
  *Success Criteria:* Intuitive drag-drop, formation templates working, save/load functionality  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` + reference existing drag-drop patterns

- [ ] **[P1] Multi-Tenant Club Setup** - Design company onboarding + branding setup  
  *Timeline:* Week 5-7  
  *Deliverable:* Interactive HTML onboarding flow in `ascendhr/design/football-club-setup/` (club name, logo upload, team structure)  
  *Success Criteria:* Setup complete in <15 minutes, multi-step wizard with state management  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` for wizard flow

- [ ] **[P1] Navigation & Layout System** - Design global navigation + page layouts  
  *Timeline:* Week 3-5  
  *Deliverable:* Unified sidebar navigation in `base.css` + HTML layout templates  
  *Success Criteria:* Consistent navigation across all HTML files, <3 clicks to any feature  
  *AI Assist:* All `.agent/rules/ascendhr-ui-designer.md` generated files use shared navigation

- [ ] **[P1] Responsive Design - Desktop** - Optimize all screens for desktop (1920px, 1440px)  
  *Timeline:* Week 6-8  
  *Deliverable:* Responsive CSS in `base.css` for key breakpoints  
  *Success Criteria:* All HTML prototypes usable on 1440px+ displays

- [ ] **[P2] Responsive Design - Tablet** - Optimize key screens for tablet (iPad)  
  *Timeline:* Week 7-9  
  *Deliverable:* Tablet media queries in `base.css` for Formation View, Player Cards  
  *Success Criteria:* Core HTML prototypes work on iPad landscape

---

### Design System Foundation

- [ ] **[P0] Color Palette & Theming** - Define brand colors + dark mode support  
  *Timeline:* Week 1-2  
  *Deliverable:* Color tokens in `ascendhr/design/design-system.md` + CSS variables in `base.css`  
  *Success Criteria:* Accessible (WCAG AA), Football Manager inspired, documented in design system  
  *Location:* `ascendhr/design/design-system.md` + `ascendhr/design/_shared/base.css`

- [ ] **[P0] Typography System** - Define font hierarchy + responsive type scale  
  *Timeline:* Week 1-2  
  *Deliverable:* Typography system in `design-system.md` + CSS variables in `base.css`  
  *Success Criteria:* Readable at all sizes, clear hierarchy, used in all HTML prototypes  
  *Location:* `ascendhr/design/design-system.md` + `ascendhr/design/_shared/base.css`

- [ ] **[P0] Component Library - Basics** - Design core components (buttons, forms, cards)  
  *Timeline:* Week 2-4  
  *Deliverable:* CSS component classes in `base.css` (buttons, forms, cards, modals, tables)  
  *Success Criteria:* 20+ reusable CSS components, documented in `design-system.md`, used across all HTML files  
  *Location:* `ascendhr/design/_shared/base.css`

- [ ] **[P1] Icon Set Design** - Create custom icon set (Football Manager theme)  
  *Timeline:* Week 3-5  
  *Deliverable:* 50+ SVG icons in `ascendhr/design/_shared/icons/` or icon font  
  *Success Criteria:* All UI needs covered, 24px grid, used in HTML prototypes via emoji or SVG

- [ ] **[P1] Design Tokens Setup** - Define tokens for colors, spacing, typography  
  *Timeline:* Week 3-4  
  *Deliverable:* CSS custom properties (variables) in `base.css` + documented in `design-system.md`  
  *Success Criteria:* Dev team can use CSS variables directly, consistent across all HTML files  
  *Location:* `ascendhr/design/_shared/base.css` (`:root {}` section)

- [ ] **[P2] Component Documentation** - Document usage guidelines for components  
  *Timeline:* Week 6-8  
  *Deliverable:* Component documentation in `ascendhr/design/design-system.md` with HTML examples  
  *Success Criteria:* Designers and devs understand usage, includes code snippets

---

### Branding & Visual Identity

- [ ] **[P0] Logo Design** - Create AscendHR logo (Football Manager inspired)  
  *Timeline:* Week 1-3  
  *Deliverable:* Logo in multiple formats (SVG, PNG, variations)  
  *Success Criteria:* Professional, memorable, works at all sizes

- [ ] **[P0] Brand Guidelines v1.0** - Define brand voice, tone, visual style  
  *Timeline:* Week 3-5  
  *Deliverable:* Brand guidelines PDF (logo usage, colors, typography)  
  *Success Criteria:* Consistent brand application across platform

- [ ] **[P1] Club Theming System** - Design customizable club branding for customers  
  *Timeline:* Week 5-7  
  *Deliverable:* Theme configuration interface + preview  
  *Success Criteria:* Customers can upload logo, set colors

- [ ] **[P2] Illustration Style Guide** - Define illustration style for empty states, onboarding  
  *Timeline:* Week 6-8  
  *Deliverable:* 5-10 illustrations + style guide  
  *Success Criteria:* Consistent style, on-brand

---

### Prototyping & Validation

- [ ] **[P0] Interactive Prototype - Core Flows** - Create clickable prototype for key features  
  *Timeline:* Week 5-7  
  *Deliverable:* Interactive HTML prototypes for 5+ user flows (linked together via navigation)  
  *Success Criteria:* Realistic interactions, buttons work, modals open/close, ready for usability testing  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` to generate from Mermaid flows  
  *Location:* `ascendhr/design/{feature}/`

- [ ] **[P0] Internal Usability Testing** - Test HTML prototypes with internal team  
  *Timeline:* Week 6-8  
  *Deliverable:* Usability test report (Markdown) with findings + recommendations + video recordings  
  *Success Criteria:* 5+ users tested, 15+ actionable insights, issues logged in Mermaid edge-case-matrix.md

- [ ] **[P0] Design Iteration - Post-Testing** - Refine HTML prototypes based on feedback  
  *Timeline:* Week 7-9  
  *Deliverable:* Updated HTML files in `ascendhr/design/{feature}/` addressing top 10 issues  
  *Success Criteria:* Critical UX issues resolved, changes documented in Mermaid flows  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` to regenerate affected screens

- [ ] **[P1] Design QA - Pre-Launch** - Review all HTML prototypes for consistency and quality  
  *Timeline:* Week 9-10  
  *Deliverable:* QA checklist (Markdown) completed + bug list  
  *Success Criteria:* Zero critical design bugs, consistent styling via `base.css`, all navigation links work

---

## Phase 2: ⚡ AI Recruitment & Evaluation (6-8 weeks + 4 weeks GTM)

**Goal:** Design AI integration UX, evaluation system, optimize for beta customers

**Design Milestones:**
- AI recruitment flow designed and intuitive
- Evaluation system UX validated
- Beta customer onboarding optimized

---

### AI Integration UX

- [ ] **[P0] TechVue Data Visualization** - Design how AI assessment data displays  
  *Timeline:* Week 1-3  
  *Deliverable:* HTML mockups in `ascendhr/design/ai-integration/` showing TechVue scores as Player Card attributes  
  *Success Criteria:* External data clearly distinguished from manual ratings  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` for data visualization patterns

- [ ] **[P0] Attribute Mapping Interface** - Design tool to map external scores to 1-20 scale  
  *Timeline:* Week 2-3  
  *Deliverable:* Interactive HTML configuration interface in `ascendhr/design/ai-integration/`  
  *Success Criteria:* HR can set mapping rules without dev help, form validation works  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` for complex form patterns

- [ ] **[P0] AI Fit Scoring Display** - Design candidate match % visualization  
  *Timeline:* Week 2-4  
  *Deliverable:* HTML fit score UI in `ascendhr/design/scouting-network/` on candidate cards + detailed breakdown  
  *Success Criteria:* Match reasoning clear, trust-building, interactive tooltip explanations  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` for data visualization

- [ ] **[P0] Unified Candidate Dashboard** - Design consolidated view of AI data  
  *Timeline:* Week 3-5  
  *Deliverable:* Dashboard mockups with filters, sorting, comparison  
  *Success Criteria:* Compare 3+ candidates side-by-side

- [ ] **[P1] Webhook Status Indicators** - Design real-time sync status UI  
  *Timeline:* Week 3-4  
  *Deliverable:* Status indicators + error states  
  *Success Criteria:* Users understand when data is syncing

---

### Evaluation System Design

- [ ] **[P0] Annual Review Workflow** - Design end-to-end evaluation process  
  *Timeline:* Week 3-5  
  *Deliverable:* Evaluation flow mockups (start → complete → attribute update)  
  *Success Criteria:* Complete review in <15 minutes

- [ ] **[P0] Attribute Update Interface** - Design post-review attribute editing  
  *Timeline:* Week 4-5  
  *Deliverable:* Bulk attribute update UI with before/after comparison  
  *Success Criteria:* Update 10+ attributes efficiently

- [ ] **[P1] 360-Degree Feedback Forms** - Design multi-rater input collection  
  *Timeline:* Week 5-6  
  *Deliverable:* Feedback form UI + aggregation view  
  *Success Criteria:* Easy for peers to provide input

- [ ] **[P1] Evaluation Dashboard** - Design manager view of team evaluation progress  
  *Timeline:* Week 5-6  
  *Deliverable:* Dashboard showing completion status, overdue reviews  
  *Success Criteria:* Managers can track 20+ evaluations

---

### Notification & Engagement

- [ ] **[P0] Email Digest Templates** - Design weekly notification emails  
  *Timeline:* Week 4-6  
  *Deliverable:* HTML email templates in `ascendhr/design/emails/` (attribute updates, evaluation reminders)  
  *Success Criteria:* >40% open rate, clear CTAs, mobile-responsive  
  *Note:* Use inline CSS for email compatibility

- [ ] **[P1] In-App Notification System** - Design notification center + toasts  
  *Timeline:* Week 5-7  
  *Deliverable:* Notification UI mockups + interaction states  
  *Success Criteria:* Non-intrusive, actionable

- [ ] **[P1] 1-on-1 Meeting Tracker** - Design simple meeting log UI  
  *Timeline:* Week 6-7  
  *Deliverable:* Meeting tracker mockups with notes + action items  
  *Success Criteria:* Log meeting in <2 minutes

---

### Beta Customer Experience

- [ ] **[P0] Beta Onboarding Flow** - Design optimized first-time user experience  
  *Timeline:* Week 1-3 (GTM prep)  
  *Deliverable:* Interactive HTML onboarding flow in `ascendhr/design/onboarding/` with progress indicators  
  *Success Criteria:* Time-to-first-value <10 minutes, multi-step wizard with state management  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` for wizard pattern

- [ ] **[P0] Interactive Tutorials** - Design in-app walkthroughs for key features  
  *Timeline:* Week 2-4 (GTM prep)  
  *Deliverable:* Tutorial overlay HTML/CSS in `ascendhr/design/tutorials/` + tooltips for 5+ features  
  *Success Criteria:* 80%+ tutorial completion rate, skip functionality  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` for overlay patterns

- [ ] **[P1] Help Documentation Design** - Design help center UI + article templates  
  *Timeline:* Week 3-5  
  *Deliverable:* HTML help center in `ascendhr/design/help-center/` + 10+ article templates (Markdown)  
  *Success Criteria:* Easy to search, clear visual aids, responsive  
  *AI Assist:* Use `.agent/rules/ascendhr-ui-designer.md` for documentation layout

- [ ] **[P1] Customer Feedback Collection** - Design in-app feedback widget  
  *Timeline:* Week 4-5  
  *Deliverable:* Feedback form + NPS survey UI  
  *Success Criteria:* <30 second feedback submission

---

### UX Optimization

- [ ] **[P0] Beta Usability Testing** - Test HTML prototypes with 3-5 beta customers  
  *Timeline:* Week 4-8 (during beta)  
  *Deliverable:* Usability reports (Markdown) with video recordings + insights  
  *Success Criteria:* 10+ usability issues identified and prioritized, logged in `ascendhr/ux/{feature}/edge-case-matrix.md`

- [ ] **[P0] Design Iteration - Beta Feedback** - Refine based on beta customer feedback  
  *Timeline:* Week 6-10  
  *Deliverable:* Updated designs addressing top 15 beta issues  
  *Success Criteria:* NPS improves by 10+ points

- [ ] **[P1] Analytics Dashboard Design** - Design internal dashboard to track usage  
  *Timeline:* Week 5-7  
  *Deliverable:* Analytics dashboard mockups (feature usage, engagement)  
  *Success Criteria:* Product team can track key metrics

---

## Phase 3: 🎓 Social + Progress Engine (8-10 weeks + 12 weeks GTM)

**Goal:** Design social features, marketing website, sales materials for market launch

**Design Milestones:**
- Social features designed and engaging
- Marketing website launched
- Sales enablement materials ready

---

### Social Features Design

- [ ] **[P0] Recognition Feed/Kudos System** - Design social recognition interface  
  *Timeline:* Week 1-4 (feature dev)  
  *Deliverable:* Feed UI + kudos giving flow + notification design  
  *Success Criteria:* Give kudos in <30 seconds, feed engaging

- [ ] **[P0] Team Performance Dashboard** - Design OKR tracking + progress visualization  
  *Timeline:* Week 2-5 (feature dev)  
  *Deliverable:* Dashboard with goals, progress bars, team metrics  
  *Success Criteria:* Managers check weekly, clear progress

- [ ] **[P0] Progress Visualization** - Design attribute trend charts + skill heatmaps  
  *Timeline:* Week 3-6 (feature dev)  
  *Deliverable:* Chart designs + data visualization mockups  
  *Success Criteria:* Growth clearly visible, motivating

- [ ] **[P1] Training Completion Workflow** - Design training log + attribute update flow  
  *Timeline:* Week 4-7 (feature dev)  
  *Deliverable:* Training notification + completion UI  
  *Success Criteria:* Log training in <3 minutes

- [ ] **[P1] Development Plan Templates** - Design plan builder + progress tracking  
  *Timeline:* Week 5-8 (feature dev)  
  *Deliverable:* Plan creation UI + milestone tracking  
  *Success Criteria:* Create plan in <10 minutes using templates

---

### Marketing Website Design

- [ ] **[P0] Homepage Design** - Design hero, features, pricing, testimonials, footer  
  *Timeline:* Week 1-4 (GTM prep)  
  *Deliverable:* High-fidelity homepage mockups (desktop + mobile)  
  *Success Criteria:* Clear value prop, <3s to understand product

- [ ] **[P0] Product Feature Pages** - Design detailed pages for core features  
  *Timeline:* Week 2-5 (GTM prep)  
  *Deliverable:* 4+ feature pages with screenshots, benefits, use cases  
  *Success Criteria:* SEO-optimized, conversion-focused

- [ ] **[P0] Pricing Page Design** - Design tier comparison + CTA  
  *Timeline:* Week 3-5 (GTM prep)  
  *Deliverable:* Pricing page with feature comparison table  
  *Success Criteria:* Clear differentiation, easy to choose tier

- [ ] **[P0] Demo Booking Flow** - Design demo request form + confirmation  
  *Timeline:* Week 3-4 (GTM prep)  
  *Deliverable:* Demo booking UI + thank you page  
  *Success Criteria:* <2 min to book demo

- [ ] **[P1] Case Study Page Templates** - Design case study layout  
  *Timeline:* Week 4-6 (GTM prep)  
  *Deliverable:* Case study page template with metrics, quotes, screenshots  
  *Success Criteria:* Professional, credible, conversion-focused

- [ ] **[P1] Blog Template Design** - Design blog post layout for content marketing  
  *Timeline:* Week 5-7  
  *Deliverable:* Blog post template + category pages  
  *Success Criteria:* Readable, shareable, on-brand

- [ ] **[P2] About/Team Page** - Design company story + team member profiles  
  *Timeline:* Week 6-8  
  *Deliverable:* About page mockups  
  *Success Criteria:* Builds trust, humanizes brand

---

### Sales Enablement

- [ ] **[P0] Pitch Deck Design** - Design 15-20 slide sales presentation  
  *Timeline:* Week 1-3 (GTM prep)  
  *Deliverable:* PowerPoint/Keynote deck with custom graphics  
  *Success Criteria:* Founder can deliver 30-min pitch

- [ ] **[P0] Demo Environment Setup** - Design demo account data + scenarios  
  *Timeline:* Week 2-4 (GTM prep)  
  *Deliverable:* Demo data specification + sample screenshots  
  *Success Criteria:* Realistic demo data, covers all features

- [ ] **[P0] Product Screenshots** - Create marketing-quality screenshots  
  *Timeline:* Week 3-5 (GTM prep)  
  *Deliverable:* 20+ high-res screenshots for website/sales  
  *Success Criteria:* Professional, realistic data, branded

- [ ] **[P1] Sales Collateral Design** - Design one-pagers, brochures, leave-behinds  
  *Timeline:* Week 4-6  
  *Deliverable:* PDF sales materials (1-pager, feature comparison)  
  *Success Criteria:* Print-ready, branded, persuasive

- [ ] **[P1] Product Video Storyboards** - Design video tutorial scripts/storyboards  
  *Timeline:* Week 5-7  
  *Deliverable:* Storyboards for 3-5 feature videos  
  *Success Criteria:* <2 min videos, clear demonstrations

---

### Customer Success Design

- [ ] **[P0] Customer Onboarding Checklist** - Design first-week onboarding experience  
  *Timeline:* Week 1-4 (GTM prep)  
  *Deliverable:* Onboarding checklist UI + progress tracking  
  *Success Criteria:* 80%+ complete all steps

- [ ] **[P0] Interactive Tutorial Videos** - Create Loom/video tutorials  
  *Timeline:* Week 3-6  
  *Deliverable:* 5-10 feature tutorial videos (2-5 min each)  
  *Success Criteria:* <30% support tickets on covered topics

- [ ] **[P1] Help Center - Full Build** - Design comprehensive help center  
  *Timeline:* Week 4-8  
  *Deliverable:* Help center with 30+ articles, search, categories  
  *Success Criteria:* 50%+ of questions answered via help center

- [ ] **[P1] Email Templates - Customer Success** - Design onboarding, check-in, renewal emails  
  *Timeline:* Week 5-7  
  *Deliverable:* 10+ HTML email templates  
  *Success Criteria:* >30% open rate, clear next actions

---

### Growth Marketing Assets

- [ ] **[P0] LinkedIn Content Graphics** - Design post templates for Thai HR content  
  *Timeline:* Week 1-12 (ongoing GTM)  
  *Deliverable:* 20+ LinkedIn graphic templates  
  *Success Criteria:* On-brand, engaging, reusable

- [ ] **[P0] Product Hunt Launch Assets** - Design PH page, graphics, promo materials  
  *Timeline:* Week 2-3 (GTM launch)  
  *Deliverable:* Product Hunt gallery images, logo, tagline graphics  
  *Success Criteria:* Ready for PH launch day

- [ ] **[P1] Blog Post Graphics** - Design featured images + inline graphics  
  *Timeline:* Week 2-12 (ongoing GTM)  
  *Deliverable:* Template + 10+ custom blog graphics  
  *Success Criteria:* Shareable, SEO-optimized

- [ ] **[P1] Email Campaign Templates** - Design drip campaign emails  
  *Timeline:* Week 4-8  
  *Deliverable:* Trial nurture sequence (5-7 emails)  
  *Success Criteria:* >25% open rate, >5% click rate

- [ ] **[P1] Social Media Assets** - Design Facebook, Twitter, Instagram graphics  
  *Timeline:* Week 5-10  
  *Deliverable:* 20+ social media graphics (announcements, tips, features)  
  *Success Criteria:* Consistent brand presence

- [ ] **[P2] Event Materials** - Design booth graphics, business cards, stickers  
  *Timeline:* Week 8-12  
  *Deliverable:* Event booth design + swag mockups  
  *Success Criteria:* Professional, memorable

---

## Phase 4: 🎯 Predictive Alerts Engine (8-10 weeks)

**Goal:** Design executive dashboards, predictive analytics UI, premium features

**Design Milestones:**
- Executive dashboards intuitive and impactful
- Predictive alerts clear and actionable
- Premium tier visually differentiated

---

### Executive Dashboards

- [ ] **[P0] ROI Calculator Design** - Design interactive ROI calculation tool  
  *Timeline:* Week 1-3  
  *Deliverable:* Calculator UI with inputs, real-time calculations, export  
  *Success Criteria:* Used in 100% of executive demos

- [ ] **[P0] Executive Dashboard - C-Suite** - Design high-level view for CEOs  
  *Timeline:* Week 2-4  
  *Deliverable:* Dashboard showing team health, flight risk, ROI at a glance  
  *Success Criteria:* Execs understand in <1 minute

- [ ] **[P0] Board Presentation Templates** - Design exportable presentation views  
  *Timeline:* Week 3-5  
  *Deliverable:* One-click PowerPoint/PDF export templates  
  *Success Criteria:* Professional, ready for board meetings

- [ ] **[P1] Executive Sales Deck** - Design ROI-focused pitch for C-suite  
  *Timeline:* Week 2-4  
  *Deliverable:* 10-slide executive pitch deck  
  *Success Criteria:* Focuses on business value, ROI proof

---

### Predictive Analytics UI

- [ ] **[P0] Flight Risk Alerts Design** - Design urgent alert UI for high-risk employees  
  *Timeline:* Week 1-3  
  *Deliverable:* Alert card design + detail view + action recommendations  
  *Success Criteria:* Urgency clear, actions obvious

- [ ] **[P0] Weekly Analytics Digest** - Design email summary template  
  *Timeline:* Week 2-4  
  *Deliverable:* Email template with insights, trends, action items  
  *Success Criteria:* <2 min to read, actionable insights

- [ ] **[P0] Burnout Detection Interface** - Design burnout warning visualization  
  *Timeline:* Week 2-4  
  *Deliverable:* Burnout indicators on Player Cards + alert dashboard  
  *Success Criteria:* Early warning signals clear

- [ ] **[P1] Trend & Anomaly Visualization** - Design charts for unusual patterns  
  *Timeline:* Week 3-5  
  *Deliverable:* Interactive charts with anomaly highlights  
  *Success Criteria:* Anomalies obvious, drill-down possible

- [ ] **[P1] Predictive Scoring Interfaces** - Design risk score displays  
  *Timeline:* Week 4-6  
  *Deliverable:* Score visualization + contributing factors breakdown  
  *Success Criteria:* Scores trusted, reasoning transparent

---

### Business ROI Dashboards

- [ ] **[P0] Retention ROI Dashboard** - Design cost savings visualization  
  *Timeline:* Week 2-4  
  *Deliverable:* Dashboard showing retention vs turnover costs  
  *Success Criteria:* Clear ฿ savings shown

- [ ] **[P0] Hiring Efficiency Dashboard** - Design time-to-hire + cost metrics  
  *Timeline:* Week 3-5  
  *Deliverable:* Dashboard with benchmarks, trends, savings  
  *Success Criteria:* Proves platform ROI

- [ ] **[P1] Training ROI Visualization** - Design training investment → outcome metrics  
  *Timeline:* Week 4-6  
  *Deliverable:* ROI calculator for training programs  
  *Success Criteria:* Links training to attribute improvement

---

### Premium Features & Upsell

- [ ] **[P0] Feature Gating Design** - Design premium tier visual indicators  
  *Timeline:* Week 1-3  
  *Deliverable:* Premium badges, locked state UI, upsell prompts  
  *Success Criteria:* Clear differentiation, not annoying

- [ ] **[P1] Upsell Prompt Design** - Design in-app upgrade prompts  
  *Timeline:* Week 3-5  
  *Deliverable:* Contextual upsell UI for Phase 4 features  
  *Success Criteria:* >10% click-through to pricing page

- [ ] **[P1] Feature Comparison Table** - Design tier comparison for customers  
  *Timeline:* Week 3-5  
  *Deliverable:* Interactive comparison table  
  *Success Criteria:* Clear what each tier includes

---

### Scale & Polish

- [ ] **[P0] Design System v2.0** - Refine component library based on learnings  
  *Timeline:* Week 4-6  
  *Deliverable:* Updated Figma library with new patterns  
  *Success Criteria:* 50+ refined components, well documented

- [ ] **[P0] Accessibility Audit** - Review platform for WCAG compliance  
  *Timeline:* Week 5-7  
  *Deliverable:* Accessibility report + remediation designs  
  *Success Criteria:* WCAG AA compliant

- [ ] **[P1] Mobile Responsive Optimization** - Polish mobile experience  
  *Timeline:* Week 5-8  
  *Deliverable:* Mobile mockups for all key screens  
  *Success Criteria:* Core features work on mobile

- [ ] **[P1] Animation & Micro-interactions** - Design delightful interactions  
  *Timeline:* Week 6-8  
  *Deliverable:* Animation specs + Lottie files  
  *Success Criteria:* Platform feels polished, fast

- [ ] **[P2] Dark Mode Refinement** - Polish dark mode across platform  
  *Timeline:* Week 7-9  
  *Deliverable:* Dark mode audit + refinements  
  *Success Criteria:* Consistent, accessible dark mode

---

## 🔄 Continuous Activities (All Phases)

**Ongoing design tasks that span multiple phases:**

### Design Operations
- [ ] **Weekly Design Reviews** - Critique sessions with product/dev team  
- [ ] **Design Handoff** - Prepare specs and assets for dev team  
- [ ] **Design QA** - Review implemented designs, log bugs  

### User Research
- [ ] **Monthly User Interviews** - Conduct 2-3 customer interviews per month  
- [ ] **Usability Testing** - Test new features with 3-5 users before launch  
- [ ] **Analytics Review** - Review usage data to identify UX improvements  

### Design System Maintenance
- [ ] **Component Updates** - Add new components as needed  
- [ ] **Documentation Updates** - Keep design system docs current  
- [ ] **Version Control** - Maintain Figma file organization  

### Brand & Marketing
- [ ] **Marketing Asset Creation** - Design graphics for campaigns  
- [ ] **Social Media Graphics** - Create weekly social content  
- [ ] **Sales Collateral Updates** - Keep pitch deck/materials current  

---

## 📊 Success Metrics by Phase

| Phase | Key Design Metrics | Target |
|-------|-------------------|--------|
| **Phase 1** | Core features designed | 100% |
| | Internal usability score | 8+/10 |
| | Design system completeness | 80%+ |
| **Phase 2** | Beta customer NPS (design) | 50+ |
| | Onboarding completion | 80%+ |
| | Tutorial completion rate | 70%+ |
| **Phase 3** | Marketing website conversion | 3%+ |
| | Time-to-first-value | <10 min |
| | Help center self-service | 50%+ |
| **Phase 4** | Executive dashboard clarity | 9+/10 |
| | Upsell prompt CTR | 10%+ |
| | WCAG AA compliance | 100% |

---

## 🤖 AI-Assisted Design Workflow

**How to use AI agents in this IDE:**

### UX Flow Creation
1. Create user stories in `ascendhr/user-story/{feature}.md`
2. Run AI agent with `.agent/rules/ascendhr-ux.md`
3. Agent generates comprehensive Mermaid diagrams in `ascendhr/ux/{feature}/`
4. Covers all 10 flow types (happy, error, recovery, loops, timeouts, etc.)
5. Outputs: `.mmd` files + `edge-case-matrix.md` + `README.md`

### HTML Prototype Generation
1. Use Mermaid flows from previous step
2. Read design system: `ascendhr/design/design-system.md`
3. Run AI agent with `.agent/rules/ascendhr-ui-designer.md`
4. Agent generates interactive HTML prototypes in `ascendhr/design/{feature}/`
5. Uses shared CSS: `ascendhr/design/_shared/base.css`
6. Outputs: `.html` files with working JavaScript + `README.md`

### Design System Reference
- All designs follow: `ascendhr/design/design-system.md`
- All HTML uses: `ascendhr/design/_shared/base.css`
- Component library documented with HTML examples

### Agent Rules Location
- **UX Agent:** `.agent/rules/ascendhr-ux.md`
- **UI Agent:** `.agent/rules/ascendhr-ui-designer.md`
- **PO/BA Agent:** `.agent/rules/[ascendhr]-po-ba-agent.md`
- **User Story Agent:** `.agent/rules/acendhr-user-story.md`

### Workflow Benefits
✅ **Fast iteration** - AI generates flows and HTML in minutes  
✅ **Comprehensive coverage** - All edge cases documented in Mermaid  
✅ **Developer-ready** - HTML prototypes show exact implementation  
✅ **Version-controlled** - All design work in Git  
✅ **Consistent** - Shared CSS ensures visual consistency  

---

**Document Version:** 1.0  
**Status:** Production  
**Next Review:** End of each phase  
**Owner:** Design Team Lead

**Related Documents:**
- `ascendhr/design/design-system.md` - Design system source of truth
- `ascendhr/design/_shared/base.css` - Shared component CSS
- `.agent/rules/ascendhr-ux.md` - UX flow generation agent
- `.agent/rules/ascendhr-ui-designer.md` - HTML prototype generation agent
