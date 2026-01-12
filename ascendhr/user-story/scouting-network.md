# Scouting Network (ATS-Lite) - User Stories

**Epic:** Epic 0.7 - Scouting Network (ATS-Lite)  
**Business Analysis:** [BA-scouting-network.md](./scouting-network-detail/BA-scouting-network.md)  
**Version:** 1.0  
**Created:** January 12, 2026  
**Status:** Ready for Development

---

## Overview

The Scouting Network is AscendHR's lightweight Applicant Tracking System (ATS) that brings recruitment into the same platform as team management. Inspired by Football Manager's transfer shortlist, it enables companies to track candidates with Player Card profiles and manage the complete recruitment loop from position creation to employee onboarding.

### Key Features
- 🎯 Position creation with attribute-based requirements
- 🔍 Candidate management with Player Card attributes
- 📊 Automated fit score calculation
- 📋 Kanban-based recruitment pipeline
- 💼 Interview scheduling and feedback collection
- 📝 Offer management and approval workflow
- ⚡ One-click candidate-to-employee conversion
- 📈 Source effectiveness tracking

---

## User Personas

| Persona | Role | Key Responsibilities |
|---------|------|---------------------|
| **Scout/Recruiter** | Talent Acquisition Specialist | Source candidates, manage pipeline, coordinate interviews, track recruitment metrics |
| **Hiring Manager** | Department Manager | Define position requirements, review candidates, approve offers, make final hiring decisions |
| **HR Admin** | HR Operations | Oversee all recruitment, manage sources, configure system, ensure compliance |
| **Interviewer** | Technical/Domain Expert | Conduct interviews, provide candidate feedback, make hiring recommendations |
| **Leadership** | Executive/C-Level | Strategic hiring decisions, review pipeline metrics, approve headcount |

---

## User Story Index

### Core Recruitment Loop (Must-Have - Phase 1)
- **US-4.1:** Create Position with Requirements
- **US-4.2:** Add Candidate to Scouting Network
- **US-4.3:** Calculate and Display Fit Score
- **US-4.4:** View Candidates in Kanban Board
- **US-4.5:** Move Candidate Through Pipeline Stages
- **US-4.7:** Schedule and Record Interview
- **US-4.8:** Collect Interview Feedback
- **US-4.9:** Create and Manage Job Offer
- **US-4.10:** Convert Hired Candidate to Employee

### Enhanced Features (Nice-to-Have - Phase 1)
- **US-4.6:** Conduct Screening Review
- **US-4.11:** Track and Display Source Effectiveness
- **US-4.13:** Send Email Notifications to Candidates
- **US-4.14:** View Recruitment Analytics Dashboard
- **US-4.15:** Compare Candidates Side-by-Side

### Future Enhancements (Phase 2)
- **US-4.12:** Bulk Import Candidates from CSV

---

## US-4.1: Create Position with Requirements

> **As a** Hiring Manager,  
> **I want to** create a position with specific attribute requirements,  
> **So that** I can define what skills and capabilities are needed and find candidates that fill team gaps.

### Business Context
When a manager reviews the Formation View and identifies gaps (e.g., missing Senior Backend Developer with Database expertise 16+), they need to create a position that captures these specific requirements. This position will be used to calculate fit scores for candidates and ensure hiring decisions are data-driven.

### Business Rules Applied
- **BR-001:** Position Creation Requirements
- **BR-002:** Position Requirement Weights
- **BR-018:** Position Code Auto-Generation

### Preconditions
- User has Manager or HR Admin role
- Club Setup has defined departments and teams
- Player Card System has defined attributes

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Manager reviews Formation View and identifies hiring gap | System displays current team composition |
| 2 | Manager clicks "Create Position" button | Opens position creation form |
| 3 | Manager enters position title (e.g., "Senior Backend Developer") | Validates title format |
| 4 | Manager selects department from dropdown | Displays teams within department |
| 5 | Manager optionally selects specific team | Links position to team |
| 6 | Manager selects employment type (Full-time, Contract, etc.) | Sets employment type |
| 7 | Manager sets seniority level (Junior, Mid, Senior, etc.) | Sets seniority |
| 8 | Manager enters salary range (min-max) | Validates min <= max |
| 9 | Manager enters job description in rich text editor | Saves description |
| 10 | Manager clicks "Add Requirements" | Opens attribute selection modal |
| 11 | Manager selects required attributes (e.g., Backend Development, Database Design, System Architecture) | Displays selected attributes |
| 12 | For each attribute, manager sets required score (1-20) | Shows rating slider |
| 13 | For each attribute, manager sets weight (%) | Validates total = 100% |
| 14 | System validates requirement weights sum to 100% | Shows error if not 100% or allows save |
| 15 | Manager assigns recruiter from employee list | Filters Scout role employees |
| 16 | Manager sets target start date (optional) | Saves start date |
| 17 | Manager clicks "Save as Draft" or "Open Position" | Validates all required fields |
| 18 | System generates position code (POS-2026-XXX) | Auto-increments sequence |
| 19 | If "Open Position", system validates BR-001 | Checks dept, manager, title, requirements |
| 20 | Position is created and appears in Scouting Network | Ready to receive candidates |

### Alternative Flows

**Alt 1: Copy from Template**
- Step 10a: Manager selects "Use Template" from similar position
- System pre-fills requirements from template
- Manager adjusts as needed

**Alt 2: Save as Draft**
- Step 17a: Manager saves as Draft instead of opening
- Position saved but not visible to recruiters
- Can be edited and opened later

**Alt 3: Link to Formation Position**
- Step 5a: Manager links to specific Formation View position slot
- System suggests requirements based on formation role type
- Creates bidirectional link for gap analysis

### Error Flows

**Error 1: Invalid Requirement Weights**
- Trigger: Weights don't sum to 100%
- System shows: "Position requirements weights must sum to 100%. Current total: {X}%"
- Recovery: Adjust weights, system shows remaining percentage needed

**Error 2: Missing Required Fields**
- Trigger: Attempt to open position without dept/manager/title
- System shows: "Cannot open position: Missing required fields"
- Recovery: Fill missing fields

**Error 3: No Requirements Defined**
- Trigger: Attempt to open position without requirements
- System shows: "At least one position requirement must be defined"
- Recovery: Add requirements

### Acceptance Criteria

- [ ] **Given** I am a Hiring Manager, **When** I create a position with title "Senior Backend Dev", department "Engineering", and 3 requirements totaling 100% weight, **Then** the position is created with auto-generated code POS-2026-001
- [ ] **Given** position requirements weights sum to 95%, **When** I try to save, **Then** system shows error "weights must sum to 100%"
- [ ] **Given** position is created as Draft, **When** I view Scouting Network, **Then** position is not visible to recruiters
- [ ] **Given** position is opened, **When** recruiters view positions, **Then** position appears in available positions list
- [ ] **Given** I set salary range min=80k, max=100k, **When** I save, **Then** both values are stored correctly
- [ ] **Given** I link position to Formation View slot, **When** position is created, **Then** Formation View shows open position in that slot

### UI/UX Notes

**Position Creation Form Sections:**
1. Basic Info (title, department, team, employment type, seniority)
2. Compensation (salary range)
3. Description (rich text editor with formatting)
4. Requirements (attribute selection with scores and weights)
5. Assignment (hiring manager, recruiter, target start date)

**Weight Input UX:**
- Show remaining weight percentage as user enters weights
- Visual indicator (progress bar) showing how close to 100%
- Suggest equal distribution button (divide remaining evenly)

### Integration Points
- **Formation View:** Link to formation position slots
- **Club Setup:** Load departments and teams
- **Player Card System:** Load available attributes for requirements
- **Gap Analysis:** Use gap analysis results to suggest requirements

---

## US-4.2: Add Candidate to Scouting Network

> **As a** Scout/Recruiter,  
> **I want to** add candidates to the scouting network with their Player Card attributes,  
> **So that** I can build a talent pool and evaluate candidates against position requirements.

### Business Context
Scouts source candidates from various channels (LinkedIn, referrals, job boards) and need to add them to the system with detailed attribute ratings. These attributes will be used to calculate fit scores when candidates are matched to positions.

### Business Rules Applied
- **BR-005:** Candidate Email Uniqueness
- **BR-020:** Candidate Code Auto-Generation

### Preconditions
- User has Scout, HR Admin, or Manager role
- Sources are pre-configured in system
- Player Card attributes are defined

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Scout clicks "Add Candidate" button | Opens candidate creation form |
| 2 | Scout enters first name and last name | Validates name format |
| 3 | Scout enters email address | Validates email format and uniqueness |
| 4 | Scout enters phone number (optional) | Validates phone format |
| 5 | Scout enters LinkedIn URL (optional) | Validates URL format |
| 6 | Scout enters portfolio/website URL (optional) | Validates URL |
| 7 | Scout enters current company and title | Free text fields |
| 8 | Scout enters years of experience | Validates 0-50 range |
| 9 | Scout enters location | Free text |
| 10 | Scout selects source from dropdown (LinkedIn, Referral, etc.) | Required field |
| 11 | Scout optionally adds source details (e.g., "Referred by John Doe") | Free text |
| 12 | Scout uploads resume file (PDF, DOC, DOCX) | Validates file size < 10MB, stores in cloud |
| 13 | Scout rates candidate on Player Card attributes (1-20 scale) | Shows attribute rating sliders |
| 14 | For each attribute, scout can add notes explaining rating | Optional notes field |
| 15 | Scout sets Current Ability (overall rating 1-20) | Based on resume/initial assessment |
| 16 | Scout sets Potential Ability (growth estimate 1-20) | Estimated future capability |
| 17 | Scout clicks "Save Candidate" | Validates all required fields |
| 18 | System generates candidate code (CAN-2026-XXX) | Auto-increments sequence |
| 19 | Candidate is added to candidate pool | Available to apply to positions |
| 20 | System shows success message with candidate code | Confirmation |

### Alternative Flows

**Alt 1: Quick Add (Minimal Info)**
- Step 2a: Scout enters only name + email + source
- Saves candidate with minimal info
- Can complete attributes later when reviewing

**Alt 2: Employee Referral**
- Step 10a: Scout selects "Employee Referral" as source
- Step 11a: System prompts to select referring employee
- Links referrer for bonus tracking

**Alt 3: Import from LinkedIn**
- Step 1a: Scout pastes LinkedIn profile URL
- System pre-fills data from LinkedIn (Phase 2 feature)
- Scout reviews and confirms data

### Error Flows

**Error 1: Duplicate Email**
- Trigger: Email already exists in system
- System shows: "A candidate with email {email} already exists (ID: CAN-2026-042)"
- Recovery: Either edit email or view existing candidate profile

**Error 2: Invalid Email Format**
- Trigger: Email doesn't match valid pattern
- System shows: "Invalid email format"
- Recovery: Correct email format

**Error 3: Resume File Too Large**
- Trigger: File size > 10MB
- System shows: "Resume file must be less than 10MB"
- Recovery: Compress file or split into multiple files

**Error 4: Invalid Attribute Rating**
- Trigger: Rating outside 1-20 range
- System shows: "Attribute ratings must be between 1 and 20"
- Recovery: Adjust rating to valid range

### Acceptance Criteria

- [ ] **Given** I enter unique email "john@example.com", **When** I save candidate, **Then** candidate is created with code CAN-2026-001
- [ ] **Given** email "jane@example.com" already exists, **When** I try to save with same email, **Then** system shows duplicate error with existing candidate ID
- [ ] **Given** I upload 15MB PDF resume, **When** I try to save, **Then** system rejects file with size error
- [ ] **Given** I rate Backend Development as 18/20 with note "Strong Python skills", **When** I save, **Then** attribute and note are stored
- [ ] **Given** I set Current Ability=16, Potential=18, **When** I save, **Then** both values are stored correctly
- [ ] **Given** I select "Employee Referral" source, **When** I save, **Then** source is linked and candidate is tagged for referral bonus

### UI/UX Notes

**Candidate Form Sections:**
1. Basic Info (name, email, phone, LinkedIn, portfolio)
2. Current Role (company, title, years experience, location)
3. Source (source type, details, referrer if applicable)
4. Documents (resume upload, cover letter)
5. Player Card Attributes (attribute ratings with notes)
6. Overall Assessment (Current Ability, Potential Ability)

**Attribute Rating UX:**
- Use slider for each attribute (1-20)
- Show color coding: 1-10 red, 11-15 yellow, 16-20 green
- Allow notes per attribute for context
- Show attribute definition tooltip on hover

### Integration Points
- **Player Card System:** Use same attribute definitions as employees
- **Cloud Storage:** Store resume files securely
- **Source Management:** Link to pre-configured sources

---

## US-4.3: Calculate and Display Fit Score

> **As a** Scout/Recruiter,  
> **I want to** see an automated fit score when I match candidates to positions,  
> **So that** I can quickly identify the best candidates for each role based on objective criteria.

### Business Context
When a candidate is considered for a position, the system calculates how well their attributes match the position requirements using a weighted formula. This fit score helps prioritize candidates and make data-driven hiring decisions.

### Business Rules Applied
- **BR-003:** Fit Score Calculation
- **BR-004:** Duplicate Application Prevention
- **BR-012:** Mandatory Attribute Requirements

### Preconditions
- Position exists with defined requirements
- Candidate exists with rated attributes
- User has permission to manage applications

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Scout drags candidate card to position column in Kanban | Initiates application creation |
| 2 | System checks for duplicate application | Validates BR-004 |
| 3 | System creates Application record | Links candidate to position |
| 4 | System loads position requirements | Retrieves required attributes, scores, weights |
| 5 | System loads candidate attributes | Retrieves candidate's attribute ratings |
| 6 | System applies fit score formula | Calculates weighted percentage match |
| 7 | System stores fit_score in Application record | Saves calculated score |
| 8 | System checks mandatory requirements | Validates BR-012 |
| 9 | If mandatory requirements not met, system flags application | Shows warning icon |
| 10 | System displays fit score on application card | Color-coded percentage badge |
| 11 | User hovers over fit score | Tooltip shows attribute breakdown |
| 12 | Tooltip displays each attribute match | Shows candidate vs required for each attribute |

### Calculation Example

**Position Requirements:**
- Backend Development: Required 16, Weight 50%
- Database Design: Required 14, Weight 30%
- System Architecture: Required 12, Weight 20%

**Candidate Attributes:**
- Backend Development: 18
- Database Design: 16
- System Architecture: 10

**Fit Score Calculation:**
```
Numerator = (18 × 0.5) + (16 × 0.3) + (10 × 0.2) = 9 + 4.8 + 2 = 15.8
Denominator = (16 × 0.5) + (14 × 0.3) + (12 × 0.2) = 8 + 4.2 + 2.4 = 14.6
Fit Score = (15.8 / 14.6) × 100 = 108.2%
```

Result: 108% fit score (candidate exceeds requirements) - displayed in GREEN

### Alternative Flows

**Alt 1: Incomplete Candidate Attributes**
- Step 5a: Some attributes not rated yet
- System calculates with available attributes
- Shows warning "Fit score calculated with incomplete data"
- Displays which attributes are missing

**Alt 2: Position Requirements Changed**
- Trigger: Manager updates position requirements after applications exist
- System automatically recalculates all fit scores for that position
- Notifies recruiter of score changes

**Alt 3: Candidate Attributes Updated**
- Trigger: Scout updates candidate's attribute ratings
- System recalculates fit scores for all active applications
- Updates displayed scores in real-time

### Error Flows

**Error 1: Duplicate Application**
- Trigger: Candidate already has active application for this position
- System shows: "Candidate {name} already has an active application for this position (Status: {status})"
- Recovery: View existing application instead

**Error 2: Position Has No Requirements**
- Trigger: Position requirements not defined
- System shows: "Cannot calculate fit score: Position has no defined requirements"
- Recovery: Add requirements to position first

**Error 3: Division by Zero**
- Trigger: All required scores = 0 (invalid configuration)
- System shows: "Invalid position requirements"
- Recovery: Fix position requirements

### Acceptance Criteria

- [ ] **Given** candidate has Backend=18, Database=16, Architecture=10 and position requires Backend=16 (50%), Database=14 (30%), Architecture=12 (20%), **When** application is created, **Then** fit score = 108.2% displayed in green
- [ ] **Given** candidate has attributes below all mandatory requirements, **When** fit score is calculated, **Then** warning icon is shown on application card
- [ ] **Given** candidate is missing 2 out of 5 required attributes, **When** fit score is calculated, **Then** partial score is shown with warning "Incomplete attributes"
- [ ] **Given** I hover over fit score badge, **When** tooltip appears, **Then** I see breakdown showing each attribute: candidate score vs required
- [ ] **Given** position requirements are updated, **When** changes are saved, **Then** all application fit scores are recalculated automatically
- [ ] **Given** candidate already has active application to position, **When** I try to add again, **Then** system shows duplicate error

### UI/UX Notes

**Fit Score Display:**
- Badge on application card showing percentage
- Color coding:
  - Green: ≥ 90%
  - Yellow: 70-89%
  - Red: < 70%
- Warning icon if mandatory requirements not met

**Fit Score Tooltip:**
- Table showing each attribute
- Columns: Attribute Name | Candidate Score | Required Score | Match
- Visual indicators (✓ or ✗) for each attribute
- Overall weighted average calculation

### Integration Points
- **Player Card System:** Attribute definitions and rating scale
- **Position Requirements:** Load weights and required scores
- **Candidate Attributes:** Load candidate ratings

---

## US-4.4: View Candidates in Kanban Board

> **As a** Scout/Recruiter,  
> **I want to** view all candidates for a position in a Kanban board layout,  
> **So that** I can visualize the recruitment pipeline and see where each candidate is in the process.

### Business Context
The Kanban board is the primary interface for managing the recruitment pipeline. It provides a visual overview of all candidates and their current stage, enabling recruiters to manage multiple candidates efficiently.

### Business Rules Applied
- None specific (display/UI focused)

### Preconditions
- Position exists with status Open or Active
- User has permission to view recruitment pipeline

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Scout navigates to Scouting Network | Displays list of open positions |
| 2 | Scout selects a position | Opens Kanban board for that position |
| 3 | System displays Kanban board with columns | Shows: New, Screening, Interview, Offer, Hired |
| 4 | Each column shows count of applications | Displays number in column header |
| 5 | Applications displayed as cards in columns | Shows candidate info on each card |
| 6 | Card displays: candidate photo, name, fit score, days in stage | Visual summary |
| 7 | Fit score badge color-coded (green/yellow/red) | Based on score range |
| 8 | Scout can filter by recruiter, date range, fit score | Dynamic filtering |
| 9 | Scout can sort cards by fit score, date, name | Multiple sort options |
| 10 | Scout clicks on card | Opens candidate detail modal |

### Card Design Elements
- Candidate photo/avatar
- Full name
- Current company/title
- Fit score badge (percentage with color)
- Position title
- Days in current stage
- Source icon
- Quick action buttons (View, Schedule Interview, Reject)

### Alternative Flows

**Alt 1: Multiple Positions View**
- Step 2a: Scout views all positions in grid
- Shows mini Kanban for each position
- Click position to expand full Kanban

**Alt 2: Filter by Multiple Criteria**
- Step 8a: Scout applies multiple filters
- Filters: Recruiter + Fit Score > 80% + Last 30 days
- System shows filtered results

**Alt 3: Empty Pipeline**
- Step 3a: Position has no applications yet
- System shows empty state message
- Provides "Add Candidate" button

### Acceptance Criteria

- [ ] **Given** position has 15 applications across 5 stages, **When** I view Kanban board, **Then** all applications are displayed in correct columns
- [ ] **Given** application has fit score 95%, **When** displayed on card, **Then** badge shows "95%" in green
- [ ] **Given** candidate has been in Screening for 12 days, **When** card is shown, **Then** "12 days in stage" is displayed
- [ ] **Given** I filter by fit score > 80%, **When** filter is applied, **Then** only candidates with score ≥80% are shown
- [ ] **Given** I sort by fit score descending, **When** sort is applied, **Then** cards are ordered highest to lowest score
- [ ] **Given** position has no applications, **When** Kanban loads, **Then** empty state with "Add Candidate" button is shown

### UI/UX Notes

**Kanban Layout:**
- Horizontal scrolling for columns if needed
- Fixed column width (300px)
- Infinite scroll within columns for many cards
- Drag handles visible on hover

**Visual Hierarchy:**
- Fit score most prominent (large badge)
- Candidate name second
- Supporting info smaller

---

## US-4.5: Move Candidate Through Pipeline Stages

> **As a** Scout/Recruiter,  
> **I want to** move candidates between pipeline stages via drag-and-drop,  
> **So that** I can efficiently update candidate status as they progress through recruitment.

### Business Context
As candidates progress through screening, interviews, and offers, recruiters need to update their status in the pipeline. The drag-and-drop Kanban interface makes this fast and intuitive.

### Business Rules Applied
- **BR-006:** Application Stage Transitions
- **BR-015:** Rejection Reason Required

### Preconditions
- Application exists in Kanban board
- User has permission to manage pipeline

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Scout views Kanban board | Displays candidates in columns |
| 2 | Scout hovers over candidate card | Shows drag handle |
| 3 | Scout clicks and drags card to new column | Visual feedback during drag |
| 4 | Scout drops card in "Screening" column | Validates transition with BR-006 |
| 5 | System checks if transition is valid | Allows valid transitions only |
| 6 | If valid, system updates application.status | Changes status to new stage |
| 7 | System updates stage_updated_at timestamp | Records when change occurred |
| 8 | Card moves to new column with animation | Visual confirmation |
| 9 | Column counts update | Increments new column, decrements old |
| 10 | System logs stage change in activity timeline | Audit trail |

### Alternative Flows

**Alt 1: Bulk Move**
- Step 2a: Scout selects multiple cards (checkbox)
- Step 3a: Scout clicks "Move to..." button
- Step 4a: Scout selects target stage from dropdown
- System validates and moves all selected cards

**Alt 2: Quick Reject**
- Step 2a: Scout right-clicks on card
- Step 3a: Scout selects "Reject" from context menu
- Step 4a: System prompts for rejection reason (BR-015)
- Step 5a: Scout enters reason and confirms
- Application status → Rejected, card disappears

**Alt 3: Candidate Withdraws**
- Step 2a: Scout clicks "Candidate Withdrew" action
- System prompts for confirmation
- Application status → Withdrew, card moves to terminal state

### Error Flows

**Error 1: Invalid Transition**
- Trigger: Scout tries to move from New directly to Offer
- System shows: "Invalid stage transition: Cannot move from New to Offer"
- Recovery: Card snaps back to original column

**Error 2: Missing Screening Decision**
- Trigger: Scout tries to move from Screening to Interview without marking pass/fail
- System shows: "Please mark screening as Passed or Failed before proceeding"
- Recovery: Modal prompts for screening decision

**Error 3: Missing Interview**
- Trigger: Scout tries to move to Offer without completed interview
- System shows: "Cannot move to Offer: No completed interview found"
- Recovery: Must schedule and complete interview first

### Acceptance Criteria

- [ ] **Given** application in "New" stage, **When** I drag to "Screening", **Then** card moves and status updates to Screening
- [ ] **Given** application in "New", **When** I try to drag to "Offer", **Then** system rejects and card snaps back with error message
- [ ] **Given** application in "Screening", **When** I drag to "Interview" without screening decision, **Then** system prompts for Pass/Fail decision
- [ ] **Given** I select 5 cards and bulk move to "Screening", **When** confirmed, **Then** all 5 applications move to Screening stage
- [ ] **Given** I right-click card and select "Reject", **When** I enter reason and confirm, **Then** application is rejected and card is removed
- [ ] **Given** application moves to new stage, **When** stage_updated_at is checked, **Then** timestamp reflects current time

### UI/UX Notes

**Drag-and-Drop UX:**
- Card lifts with shadow effect during drag
- Target columns highlight on hover
- Invalid drop zones grayed out
- Smooth animation on drop
- Optimistic UI update (instant visual feedback)

**Keyboard Shortcuts:**
- Select card: Space
- Move right: →
- Move left: ←
- Reject: Delete key

---

## US-4.6: Conduct Screening Review

> **As a** Scout/Recruiter,  
> **I want to** review candidates during screening and mark them as pass or fail,  
> **So that** I can filter out unqualified candidates early in the process.

### Business Context
Initial screening (usually a phone screen or resume review) helps eliminate candidates who don't meet basic qualifications before investing time in full interviews.

### Business Rules Applied
- **BR-015:** Rejection Reason Required

### Preconditions
- Application in Screening stage
- User has Scout or HR Admin role

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Scout opens application in Screening stage | Displays candidate details and screening form |
| 2 | Scout reviews candidate resume and attributes | Shows resume and player card |
| 3 | Scout conducts phone screen or reviews materials | External activity |
| 4 | Scout clicks "Complete Screening" button | Opens screening decision form |
| 5 | Scout selects "Pass" or "Fail" | Radio buttons |
| 6 | Scout adds screening notes | Text area for observations |
| 7 | If "Fail", scout must enter rejection reason | Required field (BR-015) |
| 8 | Scout clicks "Submit Decision" | Validates required fields |
| 9 | System updates application status | Screening_Passed or Screening_Failed |
| 10 | If passed, candidate can move to Interview | Enables next stage transition |
| 11 | If failed, application moves to terminal state | Removed from active pipeline |
| 12 | System logs decision in activity timeline | Audit trail |

### Alternative Flows

**Alt 1: Request More Information**
- Step 5a: Scout selects "Need More Info"
- System sends email to candidate requesting additional information
- Application remains in Screening stage until info received

**Alt 2: On-Hold for Clarification**
- Step 5a: Scout marks as "Hold - Waiting for Hiring Manager"
- Application flagged for manager review
- Manager provides guidance, scout continues screening

### Error Flows

**Error 1: Missing Rejection Reason**
- Trigger: Scout selects "Fail" but doesn't enter reason
- System shows: "Please provide a reason for rejection"
- Recovery: Enter rejection reason in text field

### Acceptance Criteria

- [ ] **Given** application in Screening, **When** I mark as "Pass" with notes, **Then** status changes to Screening_Passed
- [ ] **Given** application in Screening, **When** I mark as "Fail" without reason, **Then** system shows error requiring rejection reason
- [ ] **Given** I mark candidate as "Fail" with reason "Insufficient experience", **When** submitted, **Then** status = Screening_Failed and reason is stored
- [ ] **Given** screening is completed, **When** I view activity timeline, **Then** screening decision and notes are logged with timestamp
- [ ] **Given** candidate is screening passed, **When** I view Kanban, **Then** candidate can be moved to Interview stage

### UI/UX Notes

**Screening Decision Modal:**
- Pass/Fail radio buttons
- Notes text area (required for all)
- Rejection reason field (conditional on Fail)
- Previous screening notes from other candidates (reference)
- Submit and Cancel buttons

---

## US-4.7: Schedule and Record Interview

> **As a** Scout/Recruiter,  
> **I want to** schedule interviews with specific interviewers,  
> **So that** candidates can be evaluated by relevant team members.

### Business Context
Interviews are the core evaluation step. Recruiters need to coordinate between candidates, interviewers, and hiring managers to schedule interview sessions.

### Business Rules Applied
- **BR-013:** Interview Scheduling Constraints

### Preconditions
- Application in Interview_Scheduled or Screening_Passed stage
- Interviewer is active employee
- User has permission to schedule interviews

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Scout opens application | Displays candidate details |
| 2 | Scout clicks "Schedule Interview" button | Opens interview scheduling form |
| 3 | Scout selects interview type (Phone, Technical, Behavioral, etc.) | Dropdown selection |
| 4 | Scout selects interviewer from employee list | Filtered list of active employees |
| 5 | Scout sets date and time | Date/time picker, validates future date (BR-013) |
| 6 | Scout sets duration (15-480 minutes) | Number input with validation |
| 7 | Scout enters location/meeting link (Zoom, Meet, Office) | Text field |
| 8 | Scout adds interview notes/instructions (optional) | Text area |
| 9 | Scout clicks "Schedule Interview" | Validates all required fields |
| 10 | System creates Interview record with status=Scheduled | Stores in database |
| 11 | System sends calendar invite to interviewer | Email with .ics attachment |
| 12 | System optionally sends confirmation to candidate | Candidate communication |
| 13 | Interview appears in candidate's interview list | Displayed with status |
| 14 | Application status updates to Interview_Scheduled | Stage transition |

### Alternative Flows

**Alt 1: Multiple Interview Rounds**
- Step 2a: Scout schedules multiple interviews
- Technical interview with Engineer A
- Behavioral interview with Manager B
- Final interview with Director C
- All interviews tracked separately

**Alt 2: Panel Interview**
- Step 4a: Scout selects multiple interviewers
- System creates separate Interview records for each
- All interviewers receive calendar invite
- Each can submit individual feedback

**Alt 3: Reschedule Interview**
- Trigger: Interviewer or candidate requests change
- Scout clicks "Reschedule" on existing interview
- Updates date/time, status remains Scheduled
- New calendar invite sent

### Error Flows

**Error 1: Interview in Past**
- Trigger: Scout selects date/time in the past
- System shows: "Cannot schedule interview: Date must be in the future"
- Recovery: Select future date/time

**Error 2: Interviewer Not Active**
- Trigger: Selected interviewer is inactive/terminated
- System shows: "Selected interviewer is not an active employee"
- Recovery: Select different interviewer

**Error 3: Duration Out of Range**
- Trigger: Duration < 15 min or > 480 min
- System shows: "Interview duration must be between 15 and 480 minutes"
- Recovery: Adjust duration to valid range

### Acceptance Criteria

- [ ] **Given** I select Technical interview type, interviewer John, date 2026-02-15 14:00, duration 60min, **When** I schedule, **Then** Interview record is created with status=Scheduled
- [ ] **Given** I try to schedule interview for yesterday, **When** I submit, **Then** system shows error "Date must be in the future"
- [ ] **Given** interview is scheduled, **When** created, **Then** interviewer receives calendar invite email
- [ ] **Given** I schedule 3 separate interviews for same candidate, **When** all scheduled, **Then** all 3 appear in candidate's interview list
- [ ] **Given** I reschedule interview from Feb 15 to Feb 20, **When** updated, **Then** new calendar invite is sent with updated time

### UI/UX Notes

**Interview Scheduling Form:**
- Interview type dropdown (Phone Screen, Technical, Behavioral, Culture Fit, Final)
- Interviewer selector (autocomplete search)
- Date/time picker (calendar widget)
- Duration presets (30min, 45min, 60min, 90min, custom)
- Location/link field with Zoom/Meet quick-add buttons
- Notes section for interview focus areas

**Interview List Display:**
- Show all interviews for candidate
- Status badges (Scheduled, Completed, Cancelled, No-Show)
- Quick actions (Reschedule, Cancel, Complete)

---

## US-4.8: Collect Interview Feedback

> **As an** Interviewer,  
> **I want to** submit feedback and recommendations after conducting an interview,  
> **So that** hiring managers can make informed decisions based on my assessment.

### Business Context
After conducting an interview, interviewers need to provide structured feedback including strengths, concerns, ratings, and hiring recommendations. This feedback is critical for the hiring decision.

### Business Rules Applied
- **BR-007:** Interview Completion Requirements

### Preconditions
- Interview exists with status=Scheduled
- Interview date/time has passed
- User is assigned interviewer

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Interviewer receives notification to complete feedback | Email reminder after interview time |
| 2 | Interviewer opens application | Shows candidate details and interview info |
| 3 | Interviewer clicks "Complete Interview" button | Opens feedback form |
| 4 | Interviewer writes detailed feedback in text area | Rich text editor |
| 5 | Interviewer notes candidate strengths | Free text |
| 6 | Interviewer notes candidate concerns/weaknesses | Free text |
| 7 | Interviewer rates overall interview (1-5 stars) | Star rating component |
| 8 | Interviewer sets recommendation | Dropdown: Strong Hire, Hire, Maybe, No Hire |
| 9 | Interviewer adds any additional notes | Optional field |
| 10 | Interviewer clicks "Submit Feedback" | Validates required fields (BR-007) |
| 11 | System validates feedback and recommendation are provided | Enforces BR-007 |
| 12 | System updates interview.status = Completed | Marks interview done |
| 13 | System records completion timestamp | interview.completed_at |
| 14 | System appends feedback summary to application.notes | Makes visible to hiring team |
| 15 | System notifies hiring manager | Email notification |
| 16 | Hiring manager can now review feedback | Enables offer decision |

### Alternative Flows

**Alt 1: Interview Cancelled**
- Step 3a: Interviewer clicks "Cancel Interview"
- System prompts for cancellation reason
- Interview status = Cancelled
- Recruiter notified to reschedule

**Alt 2: Candidate No-Show**
- Step 3a: Interviewer clicks "Candidate No-Show"
- System records no-show
- Interview status = No_Show
- Recruiter decides whether to reschedule or reject

**Alt 3: Request Follow-Up Interview**
- Step 8a: Recommendation = "Maybe - Need More Assessment"
- System suggests scheduling additional interview
- Interviewer can recommend specific focus areas

### Error Flows

**Error 1: Incomplete Feedback**
- Trigger: Interviewer tries to submit without feedback text
- System shows: "Cannot complete interview: Feedback and recommendation are required"
- Recovery: Enter feedback and recommendation

**Error 2: Missing Recommendation**
- Trigger: Feedback provided but no recommendation selected
- System shows: "Please select a hiring recommendation"
- Recovery: Select recommendation from dropdown

### Acceptance Criteria

- [ ] **Given** I write feedback and select "Strong Hire" recommendation, **When** I submit, **Then** interview status = Completed and feedback is stored
- [ ] **Given** I try to submit without feedback text, **When** I click submit, **Then** system shows error "Feedback and recommendation are required"
- [ ] **Given** I complete feedback, **When** submitted, **Then** hiring manager receives email notification
- [ ] **Given** feedback includes "Excellent problem-solving skills", **When** hiring manager views application, **Then** feedback is visible in application notes
- [ ] **Given** I mark candidate as "No-Show", **When** confirmed, **Then** interview status = No_Show and recruiter is notified

### UI/UX Notes

**Feedback Form Sections:**
1. Interview Details (read-only: date, type, duration)
2. Detailed Feedback (rich text editor with formatting)
3. Strengths (bullet points or free text)
4. Concerns (bullet points or free text)
5. Overall Rating (1-5 star visual rating)
6. Recommendation (Strong Hire / Hire / Maybe / No Hire)
7. Additional Notes (optional)

**Recommendation Definitions:**
- **Strong Hire:** Exceptional candidate, hire immediately
- **Hire:** Good candidate, would be happy to have on team
- **Maybe:** Uncertain, need more information or assessment
- **No Hire:** Not suitable for this role

---

## US-4.9: Create and Manage Job Offer

> **As a** Scout/Recruiter,  
> **I want to** create and send job offers to candidates with hiring manager approval,  
> **So that** we can formally extend employment offers and track acceptance.

### Business Context
After successful interviews, the final step is creating a formal job offer with salary, start date, and employment terms. Offers require hiring manager approval before being sent to candidates.

### Business Rules Applied
- **BR-008:** Offer Salary Range Validation
- **BR-009:** Offer Approval Required
- **BR-014:** Offer Expiration

### Preconditions
- Application in Offer_Pending or Interviewed stage
- Position has defined salary range
- Hiring manager is assigned to position

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Scout opens application with positive interview feedback | Shows candidate ready for offer |
| 2 | Scout clicks "Create Offer" button | Opens offer creation form |
| 3 | System pre-fills position title and employment type | Auto-populated from position |
| 4 | System displays position salary range for reference | Shows min-max salary |
| 5 | Scout enters offered salary amount | Validates within range (BR-008) |
| 6 | Scout sets proposed start date | Date picker (future date) |
| 7 | Scout adds offer details/notes | Optional benefits, perks, etc. |
| 8 | System generates offer letter PDF from template | Populates candidate and position data |
| 9 | Scout reviews offer letter preview | Shows generated PDF |
| 10 | Scout clicks "Request Approval" | Sends to hiring manager |
| 11 | System creates Offer record with status=Draft | Stores in database |
| 12 | System notifies hiring manager for approval | Email notification |
| 13 | Hiring manager reviews offer in platform | Opens offer details |
| 14 | Manager clicks "Approve Offer" | Records approval (BR-009) |
| 15 | System validates manager is position.hiring_manager_id | Authorization check |
| 16 | Scout clicks "Send Offer to Candidate" | Final send action |
| 17 | System changes offer.status = Sent | Updates status |
| 18 | System emails offer letter PDF to candidate | Includes accept/reject links |
| 19 | System sets valid_until = current_date + 7 days | Offer expiration date |
| 20 | Application status updates to Offer_Sent | Pipeline stage change |

### Candidate Acceptance Flow

| Step | Actor | Action | System Response |
|------|-------|--------|-----------------|
| 21 | Candidate | Receives offer email | External |
| 22 | Candidate | Clicks "Accept Offer" link in email | Opens acceptance page |
| 23 | Candidate | Reviews terms and clicks "I Accept" | Confirmation required |
| 24 | System | Updates offer.status = Accepted | Records acceptance timestamp |
| 25 | System | Updates application.status = Offer_Accepted | Ready for hiring |
| 26 | System | Notifies hiring manager and recruiter | Success notification |
| 27 | Scout | Proceeds to complete hire (US-4.10) | Final conversion step |

### Alternative Flows

**Alt 1: Candidate Rejects Offer**
- Step 22a: Candidate clicks "Reject Offer" link
- System prompts for optional rejection reason
- Offer status = Rejected
- Application status = Offer_Rejected
- Recruiter notified to discuss or create revised offer

**Alt 2: Salary Negotiation**
- Step 22a: Candidate requests higher salary
- Recruiter creates revised offer with new amount
- Requires new hiring manager approval
- Old offer status = Withdrawn, new offer created

**Alt 3: Offer Expires**
- Trigger: current_date > offer.valid_until
- System cron job runs daily at midnight
- Offer status = Expired (BR-014)
- Application status = Offer_Rejected with note "Offer expired"
- Recruiter notified

**Alt 4: Company Withdraws Offer**
- Trigger: Business conditions change or position cancelled
- HR Admin clicks "Withdraw Offer"
- Offer status = Withdrawn
- Candidate notified via email

### Error Flows

**Error 1: Salary Out of Range**
- Trigger: Offered salary < min or > max
- System shows: "Offer salary ฿{amount} is outside position range ฿{min} - ฿{max}"
- Recovery: Adjust salary or update position range

**Error 2: Offer Sent Without Approval**
- Trigger: Scout tries to send before manager approval
- System shows: "Offer requires hiring manager approval before sending"
- Recovery: Wait for manager approval

**Error 3: Offer Already Exists**
- Trigger: Application already has active offer
- System shows: "Active offer already exists for this application"
- Recovery: Withdraw existing offer or edit it

### Acceptance Criteria

- [ ] **Given** position salary range is ฿80k-100k, **When** I create offer with ฿90k, **Then** offer is created successfully
- [ ] **Given** I try to create offer with ฿120k (above max), **When** I submit, **Then** system shows salary range error
- [ ] **Given** offer is created in Draft, **When** I try to send without approval, **Then** system blocks with approval required error
- [ ] **Given** hiring manager approves offer, **When** I send to candidate, **Then** offer email is sent with accept/reject links
- [ ] **Given** candidate clicks "Accept Offer", **When** confirmed, **Then** offer.status = Accepted and application.status = Offer_Accepted
- [ ] **Given** offer is sent on Jan 10 with 7-day validity, **When** Jan 18 arrives, **Then** system auto-expires offer

### UI/UX Notes

**Offer Creation Form:**
- Position details (read-only)
- Salary input (shows range for reference)
- Start date picker
- Employment type (auto-filled)
- Offer letter template selection
- Additional terms/benefits text area
- PDF preview button

**Offer Letter Template:**
- Company letterhead
- Candidate name and address
- Position title and department
- Salary and compensation details
- Start date
- Employment type and terms
- Benefits summary
- Acceptance deadline
- Accept/Reject links (for email version)

### Integration Points
- **Email Service:** Send offer letters to candidates
- **PDF Generation:** Create offer letter from template
- **Position Data:** Load salary range and employment type

---

## US-4.10: Convert Hired Candidate to Employee

> **As a** Scout/Recruiter,  
> **I want to** convert hired candidates to employees with one click,  
> **So that** the new hire seamlessly becomes part of the team in the Player Card System and Formation View.

### Business Context
This is the **critical integration point** that completes the recruitment loop. When a candidate accepts an offer and is ready to start, they must be converted from a candidate record to an employee record in the Player Card System. This conversion must be seamless and automatic, transferring all attribute data and updating Formation View.

### Business Rules Applied
- **BR-010:** Candidate to Employee Conversion (CRITICAL)
- **BR-011:** Position Closing

### Preconditions
- Application status = Offer_Accepted
- Offer exists with status = Accepted
- Player Card System API is accessible
- User has permission to complete hire

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Scout reviews offer_accepted applications | Filters applications ready for hire |
| 2 | Scout clicks "Complete Hire" button | Opens hire confirmation dialog |
| 3 | Scout confirms hire date and start date | Date confirmation from offer |
| 4 | Scout clicks "Confirm Hire" | Initiates BR-010 conversion process |
| 5 | **System creates Employee record in Player Card System** | API call to Player Card System |
| 6 | System copies candidate.first_name, last_name, email, phone | Basic info transfer |
| 7 | System copies all CandidateAttribute records → EmployeeAttribute | All 1-20 ratings transferred |
| 8 | System sets employee.department_id = position.department_id | Links to department from position |
| 9 | System sets employee.team_id = position.team_id | Links to team if specified |
| 10 | System sets employee.position_title = position.title | Job title from position |
| 11 | System sets employee.hire_date = offer.start_date | Official start date |
| 12 | System sets employee.employment_type = offer.employment_type | Full-time/Contract/etc. |
| 13 | System sets employee.salary = offer.salary_offered | Compensation |
| 14 | System sets employee.status = Active | Employee is active |
| 15 | Player Card System returns new employee_id | Successful creation |
| 16 | System updates candidate.status = Hired | Candidate converted |
| 17 | System updates candidate.employee_id = new employee ID | Bidirectional link |
| 18 | System updates candidate.hired_at = current timestamp | Track hire date |
| 19 | System updates application.status = Hired | Final application state |
| 20 | System counts hired applications for position | Query hired count |
| 21 | If hired count >= position.headcount → position.status = Filled | Close position (BR-011) |
| 22 | If position filled → All other active applications → Rejected | Bulk rejection (BR-011) |
| 23 | **System notifies Formation View of new employee** | Integration webhook/API call |
| 24 | Formation View updates to show employee in position slot | Real-time update |
| 25 | **System triggers Gap Analysis recalculation** | Updates team strength scores |
| 26 | Gap Analysis recalculates with new employee attributes | Team gaps updated |
| 27 | System updates Club Setup department headcount | Increment employee count |
| 28 | System sends welcome email to new employee | Includes login credentials |
| 29 | System notifies hiring manager of successful hire | Success notification |
| 30 | System updates recruitment analytics | Time-to-hire, source metrics |
| 31 | System creates onboarding checklist (optional) | HR tasks for new hire |
| 32 | Scout sees success confirmation | "Employee EMP-2026-XXX created successfully" |

### Alternative Flows

**Alt 1: Bulk Hire Multiple Candidates**
- Step 2a: Scout selects multiple offer_accepted applications
- Step 3a: Scout clicks "Bulk Complete Hire"
- System processes each conversion sequentially
- Shows progress for each candidate
- All successful hires trigger integrations

**Alt 2: Delayed Start Date**
- Step 3a: Start date is in future (e.g., 2 weeks from now)
- Employee created with status = Pending_Start
- System schedules activation for start_date
- On start_date, employee.status → Active automatically

**Alt 3: Returning Employee**
- Step 5a: System detects candidate email matches existing employee
- Prompts: "This candidate was previously employed. Reactivate or create new record?"
- If reactivate: Update existing employee record instead of creating new

### Error Flows

**Error 1: Offer Not Accepted**
- Trigger: Application status ≠ Offer_Accepted
- System shows: "Cannot hire: Offer has not been accepted by candidate"
- Recovery: Wait for candidate acceptance or resend offer

**Error 2: Player Card System API Failure**
- Trigger: API call to create employee fails
- System shows: "Employee creation failed: {specific error}. Contact system administrator"
- Recovery: Retry conversion, check Player Card System status, log error for debugging

**Error 3: Department No Longer Exists**
- Trigger: position.department_id was deleted
- System shows: "Cannot assign employee: Department has been deleted"
- Recovery: Restore department or manually assign employee to different department

**Error 4: Duplicate Employee Email**
- Trigger: Employee with same email already exists (not detected as returning employee)
- System shows: "Employee with this email already exists (EMP-2026-042)"
- Recovery: Verify if same person or email conflict, resolve manually

**Error 5: Formation View Integration Failure**
- Trigger: Formation View API unavailable
- System shows warning: "Employee created but Formation View not updated. Will retry automatically"
- Recovery: System queues retry, employee still created successfully

### Acceptance Criteria

- [ ] **Given** candidate "John Doe" with Backend=18, Database=17 accepted offer, **When** I complete hire, **Then** Employee record is created with same attributes
- [ ] **Given** position is for "Engineering" department, **When** candidate hired, **Then** employee.department_id = Engineering department ID
- [ ] **Given** offer start_date = 2026-03-01, **When** hired, **Then** employee.hire_date = 2026-03-01
- [ ] **Given** candidate has 5 attributes rated, **When** converted, **Then** all 5 EmployeeAttribute records are created
- [ ] **Given** position headcount = 1 and 1 candidate hired, **When** conversion completes, **Then** position.status = Filled
- [ ] **Given** position has 3 other active applications when position fills, **When** hire completes, **Then** those 3 applications are auto-rejected
- [ ] **Given** employee created successfully, **When** Formation View is checked, **Then** new employee appears in formation within 1 minute
- [ ] **Given** employee created, **When** Gap Analysis runs, **Then** team strength scores are recalculated with new employee
- [ ] **Given** conversion fails due to API error, **When** error occurs, **Then** candidate remains in Offer_Accepted state and error is logged

### Technical Implementation Notes

**API Call to Player Card System:**
```javascript
POST /api/v1/employees/from-candidate
{
  "candidate_id": "uuid",
  "position_id": "uuid", 
  "offer_id": "uuid",
  "start_date": "2026-02-01",
  "created_by": "user_uuid"
}

Response:
{
  "employee_id": "uuid",
  "employee_code": "EMP-2026-001",
  "status": "success"
}
```

**Transaction Safety:**
- Entire conversion should be transactional
- If any step fails, rollback all changes
- Candidate should not be marked Hired unless employee created successfully

**Retry Logic:**
- If Player Card API fails, queue for retry (max 3 attempts)
- If Formation View update fails, queue for async retry (non-blocking)
- If Gap Analysis fails, log but don't block (can be triggered manually)

### UI/UX Notes

**Hire Confirmation Dialog:**
- Candidate summary (name, position, fit score)
- Offer details (salary, start date)
- Checkbox: "Send welcome email to employee"
- Checkbox: "Create onboarding checklist"
- Warning: "This action cannot be undone"
- Confirm and Cancel buttons

**Success Confirmation:**
- Show employee code (EMP-2026-XXX)
- Link to view employee in Player Card System
- Link to view employee in Formation View
- Summary of updates (position filled, applications rejected, etc.)

### Integration Points (Critical)
- **Player Card System:** Create employee record with attributes
- **Formation View:** Update formation to show new employee
- **Gap Analysis:** Trigger recalculation of team gaps
- **Club Setup:** Update department headcount
- **Foundation Auth:** Create user account for employee login (optional)
- **Email Service:** Send welcome email to new employee

---

## US-4.11: Track and Display Source Effectiveness

> **As an** HR Admin,  
> **I want to** view analytics on recruitment source effectiveness,  
> **So that** I can optimize budget allocation to the most effective channels.

### Business Context
Different recruitment sources (LinkedIn, referrals, agencies) have different conversion rates and costs. Tracking source effectiveness helps optimize recruitment strategy and budget.

### Business Rules Applied
- **BR-016:** Source Effectiveness Tracking

### Preconditions
- Sources are configured in system
- Candidates have been added from various sources
- Some candidates have been hired

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | HR Admin navigates to Analytics section | Displays analytics dashboard |
| 2 | Admin clicks "Source Effectiveness" | Loads source analytics view |
| 3 | System queries all candidates grouped by source_id | Database aggregation |
| 4 | For each source, system calculates metrics | Total, Hired, Active, Rejected |
| 5 | System calculates conversion rate per source | (Hired / Total) × 100 (BR-016) |
| 6 | System loads cost_per_hire for each source | Manual cost data |
| 7 | System displays comparison table | Sortable by any column |
| 8 | Admin sorts by conversion rate descending | Identifies best sources |
| 9 | System shows trend chart over time | Line graph of monthly hires per source |
| 10 | Admin filters by date range | Refines data to specific period |
| 11 | Admin exports report to CSV/PDF | Download analytics report |

### Source Metrics Displayed

**For each source:**
- Total Candidates: COUNT(all candidates)
- Active Candidates: COUNT(status = Active)
- Hired: COUNT(status = Hired)
- Rejected: COUNT(status in rejected states)
- Conversion Rate: (Hired / Total) × 100%
- Cost per Hire: source.cost_per_hire / Hired count
- Average Time to Hire: AVG(hired_at - created_at) for hired candidates
- Top Positions: Which positions get most candidates from this source

### Alternative Flows

**Alt 1: Filter by Position**
- Step 10a: Admin filters by specific position
- Shows source effectiveness for that position only
- Helps understand which sources work best for specific roles

**Alt 2: Compare Time Periods**
- Step 10a: Admin selects two date ranges to compare
- System shows side-by-side comparison
- Highlights changes in source performance

**Alt 3: Update Source Costs**
- Step 3a: Admin clicks "Edit" on source row
- Updates cost_per_hire value
- System recalculates ROI metrics

### Acceptance Criteria

- [ ] **Given** LinkedIn source has 45 total, 9 hired, **When** I view analytics, **Then** conversion rate = 20% is displayed
- [ ] **Given** Employee Referral has 12 total, 7 hired, **When** compared to LinkedIn, **Then** referral shows 58.33% vs 20%
- [ ] **Given** I sort by conversion rate descending, **When** sorted, **Then** highest performing source appears first
- [ ] **Given** I filter by last 3 months, **When** applied, **Then** only candidates from that period are included in calculations
- [ ] **Given** I export to CSV, **When** downloaded, **Then** file contains all source metrics in tabular format

### UI/UX Notes

**Source Analytics Table:**
- Columns: Source Name, Total, Hired, Conversion %, Avg Time to Hire, Cost/Hire, ROI
- Sortable by any column
- Color coding for conversion rate (high=green, low=red)
- Expandable rows to show detail breakdown

**Trend Chart:**
- X-axis: Time (months)
- Y-axis: Number of hires
- Multiple lines (one per source)
- Interactive hover for exact values

---

## US-4.13: Send Email Notifications to Candidates

> **As a** Scout/Recruiter,  
> **I want to** send automated email notifications to candidates at key stages,  
> **So that** candidates stay informed about their application status.

### Business Context
Professional candidate communication improves candidate experience and employer brand. Automated emails at key stages keep candidates engaged.

### Email Triggers

1. **Application Received** (New stage)
2. **Screening Passed** (Moving to Interview)
3. **Interview Scheduled** (With calendar invite)
4. **Interview Reminder** (24 hours before)
5. **Offer Sent** (With offer letter)
6. **Offer Reminder** (3 days before expiration)
7. **Welcome Email** (After hire confirmation)
8. **Rejection Email** (At any rejection point)

### Main Flow

| Step | System Action | Email Content |
|------|---------------|---------------|
| 1 | Candidate added to position | "Application Received" email |
| 2 | Email includes position details | Position title, department, next steps |
| 3 | Application moves to Interview stage | "Interview Scheduled" email |
| 4 | Email includes interview details | Date, time, interviewer, location/link |
| 5 | 24 hours before interview | "Interview Reminder" email |
| 6 | Offer sent to candidate | "Job Offer" email with PDF attachment |
| 7 | 3 days before offer expires | "Offer Expiring Soon" reminder |
| 8 | Candidate hired | "Welcome to Team" email |
| 9 | Application rejected | "Application Update" email |

### Alternative Flows

**Alt 1: Per-Position Email Settings**
- Admin can enable/disable specific email types per position
- Some positions may not want automated emails
- Default: All emails OFF, must opt-in

**Alt 2: Custom Email Templates**
- Admin can customize email templates
- Use placeholders: {candidate_name}, {position_title}, {company_name}
- Preview before sending

**Alt 3: Manual Email Override**
- Recruiter can manually trigger any email
- Can edit content before sending
- Useful for special circumstances

### Acceptance Criteria

- [ ] **Given** candidate is added to position with emails enabled, **When** added, **Then** "Application Received" email is sent
- [ ] **Given** interview is scheduled, **When** created, **Then** candidate receives email with interview details
- [ ] **Given** interview is in 24 hours, **When** reminder job runs, **Then** reminder email is sent
- [ ] **Given** offer is sent, **When** status = Sent, **Then** candidate receives offer email with PDF attachment
- [ ] **Given** application is rejected, **When** status changes, **Then** rejection email is sent with reason (if provided)

---

## US-4.14: View Recruitment Analytics Dashboard

> **As an** HR Admin or Leadership,  
> **I want to** view comprehensive recruitment metrics and KPIs,  
> **So that** I can track hiring performance and identify process improvements.

### Business Context
Strategic recruitment requires data-driven decisions. The analytics dashboard provides visibility into pipeline health, efficiency metrics, and hiring trends.

### Key Metrics Displayed

**Pipeline Overview:**
- Total Open Positions
- Total Active Candidates
- Average Time to Hire
- Offer Acceptance Rate
- Positions Filled This Month/Quarter

**Funnel Metrics:**
- Conversion rates per stage (New → Screening → Interview → Offer → Hired)
- Drop-off rates at each stage
- Bottleneck identification

**Performance Metrics:**
- Average Fit Score of Hired Employees
- Time to Fill per Position
- Cost per Hire (by source)
- Recruiter Productivity (positions per recruiter)

**Trend Analysis:**
- Hires over time (monthly/quarterly)
- Pipeline velocity trends
- Source effectiveness trends

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | User navigates to Recruitment Analytics | Loads dashboard |
| 2 | System calculates all metrics | Real-time calculations |
| 3 | Dashboard displays KPI cards | Key numbers at top |
| 4 | Pipeline funnel visualization shown | Conversion rates per stage |
| 5 | Time series charts display trends | Hires over time |
| 6 | Source comparison table shown | Source effectiveness |
| 7 | User filters by date range | Updates all charts |
| 8 | User filters by department | Department-specific metrics |
| 9 | User exports dashboard to PDF | Download report |

### Acceptance Criteria

- [ ] **Given** 50 applications across 5 stages, **When** dashboard loads, **Then** funnel shows correct counts per stage
- [ ] **Given** average time-to-hire is 35 days, **When** displayed, **Then** metric card shows 35 days
- [ ] **Given** I filter by last quarter, **When** applied, **Then** all metrics update to show Q1 data only
- [ ] **Given** I export dashboard, **When** PDF generated, **Then** file includes all charts and metrics

---

## US-4.15: Compare Candidates Side-by-Side

> **As a** Hiring Manager,  
> **I want to** compare multiple candidates side-by-side,  
> **So that** I can make informed hiring decisions based on direct comparison.

### Business Context
When choosing between final candidates, hiring managers need to see detailed attribute comparisons to make the best decision.

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Manager selects 2-4 candidates | Checkbox selection |
| 2 | Manager clicks "Compare" button | Opens comparison view |
| 3 | System displays candidates in columns | Side-by-side layout |
| 4 | Each column shows candidate details | Name, fit score, experience |
| 5 | Player Card attributes displayed in rows | All attributes for comparison |
| 6 | Color coding highlights differences | Green=best, red=weakest per attribute |
| 7 | Interview feedback shown | Recommendations and ratings |
| 8 | Manager reviews and makes decision | Visual comparison |

### Acceptance Criteria

- [ ] **Given** I select 3 candidates, **When** I click Compare, **Then** all 3 appear in side-by-side columns
- [ ] **Given** Candidate A has Backend=18, B has Backend=15, **When** compared, **Then** A's value is highlighted green
- [ ] **Given** comparison view open, **When** I view interview feedback, **Then** all interviewers' recommendations are shown per candidate

---

**END OF USER STORIES DOCUMENT**
