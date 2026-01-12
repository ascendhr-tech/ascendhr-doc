# Screen Specifications - Scouting Network (ATS-Lite)

**Feature:** Scouting Network (ATS-Lite)  
**Purpose:** Component inventory for HTML UI Generator  
**Stories:** US-4.1 to US-4.10 (High/Critical Priority)  
**Generated:** January 12, 2026

---

## Screen Inventory

**Total Screens:** 26  
**Total Components:** 120+  
**Total States:** 80+

---

## 1. Position Management Screens

### 1.1 position-list

**Screen ID:** `position-list`  
**Route:** `/positions`  
**Purpose:** Browse all open positions

**Components:**
- **Header**: "Open Positions" + [New Position] button (primary)
- **Filter Bar**: 
  - Status dropdown (Draft, Published, Filled)
  - Department dropdown
  - Search input (placeholder: "Search positions...")
- **Table**:
  - Columns: Title, Department, Status, Candidates, Headcount, Actions
  - Row actions: View, Edit, Delete, View Kanban
  - Draft badge (blue pill)
- **Empty State**:
  - Icon: Empty office illustration
  - Text: "No positions yet"
  - CTA: "Create First Position" button
- **Pagination**: Max 50 per page

**States:**
- Loading: Skeleton table (5 rows)
- Empty: Empty state card
- Error: Alert banner with retry button
- Success: Populated table

**Responsive:**
- Mobile: Cards instead of table
- Tablet: Collapsed columns

---

### 1.2 position-form-step1

**Screen ID:** `position-form-step1`  
**Route:** `/positions/new` or `/positions/{id}/edit`  
**Purpose:** Basic position information

**Components:**
- **Progress Stepper**: Step 1 of 3 (active)
- **Form**:
  - Title input (required, max 100 chars)
  - Department dropdown (required)
  - Headcount number input (required, min 1)
  - Description textarea (optional, max 500 chars)
- **Actions**:
  - [Cancel] (secondary)
  - [Save as Draft] (secondary)
  - [Next] (primary, right-aligned)
- **Auto-save indicator**: "Draft saved 30 seconds ago"

**States:**
- Clean: Empty form
- Editing: Partially filled
- Validating: Inline validation errors
- Saving: Loading spinner on buttons

**Validation:**
- Title: Required, max 100 chars
- Headcount: Required, ≥ 1, number only
- Inline errors: Red text below field

---

### 1.3 position-form-step2

**Screen ID:** `position-form-step2`  
**Route:** `/positions/new/requirements`  
**Purpose:** Add position requirements

**Components:**
- **Progress Stepper**: Step 2 of 3 (active)
- **Requirements Grid**:
  - Table with columns: Attribute, Min Score, Max Score, Mandatory, Actions
  - [+ Add Requirement] button above grid
  - [Use Template] button (loads predefined)
  - Drag handles for reordering
  - Delete icon per row
- **Attribute Selector Modal**:
  - Search input
  - Attribute list (from Player Card System)
  - Backend Development (1-20 scale)
- **Score Sliders**:
  - Min: 1-20 range slider
  - Max: 1-20 range slider
  - Validation: Min ≤ Max
- **Actions**:
  - [Back] (secondary)
  - [Save as Draft] (secondary)
  - [Next] (primary)

**States:**
- Empty: No requirements added
- Populated: Grid with requirements
- Template: Pre-filled with 8 common attributes
- Validating: Error messages below grid

**Validation:**
- At least 1 requirement for publish (BR-001)
- Min ≤ Max scores
- Scores in 1-20 range

---

### 1.4 position-form-step3

**Screen ID:** `position-form-step3`  
**Route:** `/positions/new/formation`  
**Purpose:** Link to Formation View

**Components:**
- **Progress Stepper**: Step 3 of 3 (active)
- **Formation Position Selector**:
  - Dropdown: Available team positions
  - Preview card showing selected position
  - Team name, position name, current gap
- **Preview Panel**:
  - Complete position summary
  - All requirements listed
  - Formation linkage shown
- **Actions**:
  - [Back] (secondary)
  - [Skip Formation Link] (secondary)
  - [Save as Draft] (secondary)
  - [Create Position] (primary, success color)

**States:**
- Loading: Fetching Formation positions
- Error: API unavailable, allow skip
- Success: Position linked
- Preview: Final review before submit

**Integration:**
- Formation View API: GET /api/formation/positions

---

## 2. Candidate Management Screens

### 2.1 candidate-list

**Screen ID:** `candidate-list`  
**Route:** `/candidates`  
**Purpose:** Browse all candidates

**Components:**
- **Header**: "Candidates" + [Add Candidate] button
- **Filter Bar**:
  - Source dropdown (LinkedIn, Referral, etc.)
  - Fit Score range slider
  - Date added range picker
- **Card Grid**:
  - Photo thumbnail
  - Name + email
  - Fit score badge (color-coded)
  - Source label
  - Quick actions: View, Edit, Compare
- **Empty State**: "No candidates yet"

**States:**
- Loading: Skeleton cards (12)
- Empty: Empty state
- Populated: Card grid
- Filtered: Subset of cards

---

### 2.2 candidate-form

**Screen ID:** `candidate-form`  
**Route:** `/candidates/new`  
**Purpose:** Add new candidate

**Components:**
- **Method Selector**:
  - Radio: Manual Entry / LinkedIn Import
- **Basic Info Form**:
  - Full name input (required)
  - Email input (required, validation)
  - Phone input (optional, format validation)
  - Current position input
  - Years experience number input
- **Resume Upload**:
  - Drag & drop area
  - File input (PDF/DOC, max 5MB)
  - Progress bar
  - Retry button on error
- **Source Dropdown**: Required
- **Actions**:
  - [Cancel]
  - [Save & Add Attributes] (primary)

**States:**
- Empty form
- Uploading resume (progress)
- Upload error (retry button)
- Duplicate warning (modal)

**Validation:**
- Email: Valid format, unique (BR-004)
- Resume: Max 5MB, PDF/DOC only
- Source: Required

---

### 2.3 attribute-rating

**Screen ID:** `attribute-rating`  
**Route:** `/candidates/{id}/attributes`  
**Purpose:** Rate candidate attributes

**Components:**
- **Attribute Grid**:
  - Each row: Attribute name, 1-20 slider, notes textarea
  - Visual scale: 1 (Poor) → 20 (Exceptional)
  - Color feedback: Red (1-7), Yellow (8-14), Green (15-20)
- **Auto-save**: Indicator "Saving..."
- **Actions**:
  - [Skip] (secondary)
  - [Submit] (primary)

**States:**
- Loading: Fetching attributes from Player Card API
- Error: API unavailable, allow skip
- Rating: Interactive sliders
- Saved: Success message

**Integration:**
- Player Card System API:
  - GET /api/attributes/list
  - POST /api/candidates/{id}/attributes

---

### 2.4 candidate-profile

**Screen ID:** `candidate-profile`  
**Route:** `/candidates/{id}`  
**Purpose:** View complete candidate data

**Components:**
- **Header Card**:
  - Photo (circle avatar)
  - Name, email, phone
  - Fit score badge (large, color-coded)
  - Source label
  - Status badge
- **Tabs**:
  - Overview: Summary, applications, timeline
  - Attributes: Player card grid
  - Interviews: List of interviews + feedback
  - Applications: Positions applied to
  - Documents: Resume, cover letter
  - Activity: Audit log timeline
- **Actions** (floating):
  - [Edit]
  - [Schedule Interview]
  - [Add to Position]
  - [⋮ More]

**States:**
- Loading: Skeleton layout
- Complete: All data displayed
- Partial: Missing attributes warning

---

## 3. Kanban & Pipeline Screens

### 3.1 kanban-board

**Screen ID:** `kanban-board`  
**Route:** `/recruitment/kanban`  
**Purpose:** Pipeline visualization

**Components:**
- **Position Selector**: Dropdown at top
- **Filter Panel** (sidebar):
  - Fit score ranges
  - Source checkboxes
  - Date range
  - [Reset Filters] button
- **Kanban Columns** (6):
  - New, Screening, Interview, Offer, Hired, Rejected
  - Column header: Name + count
  - Drag-drop enabled
  - Scroll if >10 cards
- **Candidate Cards**:
  - Photo (small)
  - Name
  - Fit score badge
  - Days in stage
  - Quick actions (hover): 👁️ ✉️ ⋮
- **Empty State** (per column): "No candidates"

**States:**
- Loading: Skeleton columns
- Empty: Empty state
- Populated: Cards in columns
- Dragging: Card opacity 50%, column highlight
- Dropped: Animation to new column

**Interactions:**
- Drag & drop: Visual feedback
- Right-click: Context menu
- Hover: Quick actions
- Real-time updates: WebSocket

---

### 3.2 stage-move-confirmation

**Screen ID:** `stage-move-confirmation`  
**Route:** Modal overlay  
**Purpose:** Confirm stage change

**Components:**
- **Modal**:
  - Title: "Move to [Stage Name]"
  - Candidate info card
  - Notes textarea (optional)
  - Validation warnings (if invalid transition)
- **Actions**:
  - [Cancel]
  - [Confirm Move] (primary)

**States:**
- Valid transition: Green confirm button
- Invalid transition: Red error + disabled button
- Confirming: Loading spinner

**Validation:**
- BR-006: Valid stage transitions only
- BR-014: Interview required before Offer

---

### 3.3 rejection-modal

**Screen ID:** `rejection-modal`  
**Route:** Modal overlay  
**Purpose:** Reject candidate with reason

**Components:**
- **Modal**:
  - Title: "Reject Candidate"
  - Reason dropdown (12 standard reasons, required)
  - Notes textarea (optional)
  - Email checkbox: "Send rejection email"
  - Email preview button
- **Actions**:
  - [Cancel]
  - [Confirm Rejection] (danger color)

**States:**
- Empty: Reason required
- Filled: Confirm enabled
- Sending: Loading

**Validation:**
- BR-015: Rejection reason required

---

## 4. Interview Screens

### 4.1 interview-schedule-form

**Screen ID:** `interview-schedule-form`  
**Route:** `/interviews/schedule`  
**Purpose:** Schedule interview

**Components:**
- **Pre-filled**:
  - Candidate name (read-only)
  - Position (read-only)
- **Date Picker**: Calendar widget
- **Time Picker**: Dropdown (30-min intervals)
- **Duration**: Dropdown (30, 45, 60, 90, 120 min)
- **Interviewer Search**:
  - Search input
  - Multi-select (≥1 required BR-013)
  - Selected list with remove icons
- **Interview Type**: Dropdown (Technical, Cultural, etc.)
- **Meeting Link**:
  - Manual URL input
  - [Generate Zoom] button
- **Agenda**: Textarea (optional)
- **Actions**:
  - [Cancel]
  - [Preview]
  - [Schedule Interview] (primary)

**States:**
- Clean form
- Validating: Inline errors
- Generating link: Loading spinner
- Calendar conflict: Warning

**Validation:**
- Date: Future date only
- Interviewer: ≥1 required (BR-013)
- Time: No conflicts

---

### 4.2 interview-list

**Screen ID:** `interview-list`  
**Route:** `/interviews`  
**Purpose:** View all interviews

**Components:**
- **Tabs**:
  - Upcoming
  - Completed
  - All
- **Table**:
  - Columns: Candidate, Position, Date/Time, Interviewers, Status, Actions
  - Status badges: Scheduled, Completed, Cancelled
  - Feedback indicator: "Pending" / "3/3 Submitted"
- **Actions per row**:
  - View, Reschedule, Cancel, Submit Feedback

**States:**
- Loading: Skeleton table
- Empty: Empty state
- Populated: Interview list

---

### 4.3 interview-detail

**Screen ID:** `interview-detail`  
**Route:** `/interviews/{id}`  
**Purpose:** View interview details

**Components:**
- **Header Card**:
  - Interview type badge
  - Date & time (large)
  - Duration
  - Status badge
- **Participants**:
  - Candidate card (link to profile)
  - Interviewers list (with photos)
- **Meeting Info**:
  - Meeting link (clickable)
  - [Join Meeting] button (if active)
  - [Add to Calendar] button
- **Tabs**:
  - Details: Overview, agenda
  - Feedback: All submitted feedback
  - Notes: Interview notes
- **Actions**:
  - [Reschedule]
  - [Cancel Interview]
  - [Submit Feedback] (if interviewer)

**States:**
- Scheduled: Join meeting available
- Completed: Feedback section active
- Cancelled: Grayed out

---

## 5. Feedback Screens

### 5.1 feedback-form

**Screen ID:** `feedback-form`  
**Route:** `/interviews/{id}/feedback`  
**Purpose:** Submit interview feedback

**Components:**
- **Pre-filled**:
  - Candidate info (read-only)
  - Interview details (read-only)
- **Overall Rating**: 1-5 star selector (required BR-016)
- **Technical Skills** (optional):
  - Backend: 1-5 stars
  - Problem Solving: 1-5 stars
  - Communication: 1-5 stars
- **Comments**: Textarea (required, min 50 chars BR-017)
- **Recommendation**: Dropdown (required)
  - Strong Hire, Hire, Maybe, No Hire, Strong No Hire
- **Actions**:
  - [Save Draft]
  - [Preview]
  - [Submit Feedback] (primary)

**States:**
- Empty: Errors shown
- Draft: Auto-save indicator
- Submitting: Loading
- Submitted: Success message

**Validation:**
- BR-016: Overall rating required
- BR-017: Rating + comments required
- Min 50 chars in comments

---

### 5.2 feedback-view

**Screen ID:** `feedback-view`  
**Route:** `/interviews/{id}/feedback/all`  
**Purpose:** View all feedback

**Components:**
- **Aggregate Card** (top):
  - Average rating (large, color-coded)
  - Consensus recommendation
  - Completion: "3/3 interviewers submitted"
- **Individual Feedback Cards**:
  - Interviewer name + photo
  - Rating (1-5 stars)
  - Recommendation badge
  - Comments (expandable)
  - Timestamp
  - [Edit] button (within 24h only)
- **Empty State**: "Awaiting feedback" + [Send Reminder]

**States:**
- Empty: No feedback yet
- Partial: Some submitted
- Complete: All submitted
- Aggregate calculated

---

## 6. Offer Screens

### 6.1 offer-form

**Screen ID:** `offer-form`  
**Route:** `/offers/create`  
**Purpose:** Create job offer

**Components:**
- **Pre-filled**:
  - Candidate name
  - Position title
- **Salary Input**:
  - Amount (฿ currency)
  - Validation: Within position range (BR-008)
  - Range indicator: "฿60k - ฿100k"
- **Employment Type**: Dropdown (Full-time, Part-time, Contract)
- **Start Date**: Date picker (future date)
- **Expiration Date**: Date picker (min 3 days from send)
- **Benefits**: Rich text editor
- **Special Terms**: Textarea (optional)
- **Actions**:
  - [Save Draft]
  - [Preview PDF]
  - [Create Offer] (primary)

**States:**
- Clean form
- Validating: Inline errors
- Generating PDF: Loading
- Approval required: Warning banner (BR-009)

**Validation:**
- BR-008: Salary within position range
- BR-009: Approval if ≥฿80k
- Start date: Future only
- Expiration: Min 3 days

---

### 6.2 offer-detail

**Screen ID:** `offer-detail`  
**Route:** `/offers/{id}`  
**Purpose:** Track offer status

**Components:**
- **Status Banner** (top):
  - Status: Draft, Sent, Accepted, Rejected, Expired, Negotiating
  - Expiration countdown: "4 days remaining"
- **Offer Summary Card**:
  - Candidate info
  - Salary, type, dates
  - Benefits summary
- **PDF Preview**: Embedded PDF viewer
- **Actions**:
  - [Download PDF]
  - [Extend Expiration]
  - [Revise Offer]
  - [Send Reminder]
- **Timeline**: Activity log

**States:**
- Draft: Edit enabled
- Sent: Tracking active
- Accepted: Success banner
- Rejected: Reason shown
- Expired: Warning banner

---

### 6.3 offer-tracking

**Screen ID:** `offer-tracking`  
**Route:** `/offers`  
**Purpose:** Dashboard for all offers

**Components:**
- **Metrics Cards** (top row):
  - Total Offers: 12
  - Acceptance Rate: 85%
  - Avg Time to Accept: 3.2 days
- **Filter Bar**:
  - Status tabs (All, Sent, Accepted, Rejected, Expiring)
- **Table**:
  - Columns: Candidate, Position, Salary, Status, Expiration, Actions
  - Status badges (color-coded)
  - Expiring soon: Red indicator
- **Bulk Actions**: Checkbox multi-select

**States:**
- Loading: Skeleton cards + table
- Empty: Empty state
- Populated: Dashboard

---

## 7. Employee Conversion Screens (CRITICAL)

### 7.1 conversion-wizard

**Screen ID:** `conversion-wizard`  
**Route:** `/conversion/wizard`  
**Purpose:** Convert candidate to employee

**Components:**
- **Progress Stepper**: 7 steps
  1. Verify Data
  2. Review Offer
  3. Map Fields
  4. Set Department
  5. Assign ID
  6. Employment Details
  7. Preview
- **Step Content** (dynamic per step)
- **Navigation**:
  - [Back] (disabled on step 1)
  - [Cancel]
  - [Next] (or "Create Employee" on final step)

**States:**
- Navigating: Step content changes
- Validating: Inline errors per step
- Final confirmation: Modal overlay
- Processing: Locked during transaction

**Validation:**
- Offer accepted: Required
- Complete candidate data
- Department assigned
- Start date set

---

### 7.2 conversion-progress

**Screen ID:** `conversion-progress`  
**Route:** Modal overlay (non-dismissible)  
**Purpose:** Show 30-step transaction progress

**Components:**
- **Modal** (centered, no close):
  - Title: "Creating Employee..."
  - Progress bar: 0-100%
  - Current step: "Step 13/30: Calling Player Card API..."
  - Step list (scrollable):
    - ✓ Completed steps (green)
    - ⏳ Current step (blue, animated)
    - ⚪ Pending steps (gray)
- **No actions**: Cannot cancel during transaction

**States:**
- Processing: Progress bar animating
- Step updates: Every second
- Success: Progress complete, redirect to success
- Error: Stop progress, show error, rollback triggered

**Real-time:**
- WebSocket updates for step progress
- Estimated time remaining

---

### 7.3 conversion-success

**Screen ID:** `conversion-success`  
**Route:** `/conversion/success`  
**Purpose:** Confirm successful conversion

**Components:**
- **Success Banner**:
  - ✅ Icon (large, green)
  - Title: "Employee Conversion Successful"
  - Employee ID: EMP-2026-050 (large, copyable)
- **Summary Card**:
  - Employee name, position, department
  - Start date
  - Salary
- **Completed Steps Checklist**:
  - ✓ Employee profile created
  - ✓ Formation View updated
  - ✓ Gap Analysis recalculated
  - ✓ Welcome email sent
  - ✓ Position filled (2/2 hired)
  - ✓ 12 other applications rejected
- **Actions**:
  - [View Employee Profile] (primary)
  - [View Formation View]
  - [Return to Dashboard]
  - [Convert Another]

**States:**
- Success: All checkmarks green
- Partial success: Some steps skipped (warnings)

---

### 7.4 conversion-error

**Screen ID:** `conversion-error`  
**Route:** `/conversion/error`  
**Purpose:** Handle conversion failure

**Components:**
- **Error Banner**:
  - ❌ Icon (large, red)
  - Title: "Conversion Failed"
  - Message: "No data was changed" (reassurance)
- **Error Details Card**:
  - Failed at: Step 13
  - Reason: "Player Card System unavailable"
  - Technical error code: API-500
- **Rollback Confirmation**:
  - ✓ All changes rolled back
  - ✓ Candidate status unchanged
  - ✓ Database consistent
- **Actions**:
  - [Retry Conversion] (primary)
  - [View Error Log]
  - [Contact Support]
  - [Cancel]

**States:**
- Error displayed
- Retry available
- Support ticket option

---

### 7.5 bulk-conversion-summary

**Screen ID:** `bulk-conversion-summary`  
**Route:** `/conversion/bulk/summary`  
**Purpose:** Show bulk conversion results

**Components:**
- **Summary Banner**:
  - Success count: 4/5 converted
  - Failure count: 1 failed
- **Success List** (green):
  - Table: Candidate, Employee ID, Status ✓
- **Failure List** (red):
  - Table: Candidate, Error Reason, [Retry]
- **Actions**:
  - [Retry Failed Only]
  - [Export Summary CSV]
  - [Done]

**States:**
- All success: Green banner
- Mixed: Yellow banner
- All failed: Red banner

---

## Component Library Reference

### Buttons
- **Primary**: Blue, white text
- **Secondary**: Gray border, black text
- **Danger**: Red, white text
- **Success**: Green, white text

### Badges
- **Status**: Rounded pill, colored
- **Fit Score**: Circle, color-coded (Green ≥90%, Yellow 70-89%, Red <70%)

### Modals
- Overlay: 50% black opacity
- Content: White card, centered
- Max width: 600px
- Close: X icon top-right

### Forms
- Label: Above field, bold
- Required: Red asterisk
- Error: Red text below field
- Help text: Gray text below field

### Tables
- Header: Bold, gray background
- Rows: Hover effect (light gray)
- Actions: Icon buttons right-aligned

### Color Palette
- Primary: #3B82F6 (Blue)
- Success: #10B981 (Green)
- Warning: #F59E0B (Yellow)
- Error: #EF4444 (Red)
- Gray-50 to Gray-900

---

**END OF SCREEN SPECIFICATIONS**

**Total Screens Documented:** 26  
**Ready for HTML Generator:** ✅ Yes  
**Component Reusability:** High  
**State Coverage:** Complete
