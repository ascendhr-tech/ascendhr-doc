# Conduct Screening Review

**Story ID:** US-4.6  
**Epic:** Epic 0.7 - Scouting Network (ATS-Lite)  
**Persona:** Scout/Recruiter, Hiring Manager  
**Priority:** Must Have  
**Complexity:** S (1-2 days)

---

## User Story

> **As a** Scout/Recruiter,  
> **I want to** review candidate applications and mark them as passed or failed during screening,  
> **So that** only qualified candidates proceed to the interview stage.

---

## User Journey Context

### Entry Points
| Entry Source | Condition | User State |
|--------------|-----------|------------|
| Kanban board | Click "Review" on card in Screening column | Evaluating candidate |
| Application detail page | Click "Conduct Screening" button | Deep evaluation |
| Batch review interface | Multiple candidates in queue | High-volume screening |

### Exit Points
| Exit Condition | Destination | User State |
|----------------|-------------|------------|
| Screening Passed | Application moved to Interview_Scheduled | Ready to interview |
| Screening Failed | Application moved to Rejected | Pipeline cleaned |
| Save for Later | Draft saved, remains in Screening | Incomplete review |

---

## Business Logic

### Business Rules

| Rule ID | Description |
|---------|-------------|
| **BR-015** | Rejection reason required when marking as failed |
| **BR-007** | Screening decision updates application.status |

---

## Acceptance Criteria

### Scenario 1: Happy Path - Pass Screening

**Type:** ✅ Happy Path

**Given**
- Application in Screening stage
- Candidate has strong resume and fit score 92%

**When**
- I click "Conduct Screening Review"
- Review form opens with candidate details
- I select "✓ Pass Screening"
- I add notes: "Strong technical background, good communication in phone call"
- I click "Submit Decision"

**Then**
- application.status = Screening_Passed
- application.screening_decision = "Passed"
- application.screening_notes = saved
- application.screening_date = current timestamp
- Card moves to Interview-ready state
- Notification sent to hiring manager: "Alex Chen passed screening"
- Next action prompt: "Schedule Interview?"

---

### Scenario 2: Happy Path - Fail Screening

**Type:** ✅ Happy Path

**Given**
- Application in Screening stage
- Candidate lacks required experience

**When**
- I select "✗ Fail Screening"
- System prompts for rejection reason (BR-015)
- I select reason: "Insufficient experience"
- I add notes: "Only 1 year backend experience, requires 3+"
- I click "Submit Decision"

**Then**
- application.status = Screening_Failed
- application.rejection_reason = "Insufficient experience"
- application.rejected_at = current timestamp
- Card removed from active Kanban
- Optional: Send rejection email to candidate
- Position remains open for other candidates

---

### Scenario 3: Alternative Path - Save Draft Review

**Type:** 🔀 Alternative Path

**Given**
- Mid-way through screening review
- Need to check with hiring manager before deciding

**When**
- I add notes but don't select Pass/Fail
- I click "Save Draft"

**Then**
- Notes saved as draft
- application.status remains Screening (unchanged)
- Draft indicator shown on card
- Can resume later with pre-filled notes

---

### Scenario 4: Validation Error - No Rejection Reason

**Type:** ❌ Validation Error

**Given**
- I select "Fail Screening"
- I skip rejection reason field

**When**
- I click "Submit Decision"

**Then**
- Error: "Rejection reason is required (BR-015)"
- Form not submitted
- Rejection reason field highlighted

---

### Scenario 5: Permission Denied - Interviewer Cannot Screen

**Type:** 🔒 Permission Denied

**Given**
- I am logged in as Interviewer (not Recruiter)

**When**
- I attempt to conduct screening review

**Then**
- Error: "Only recruiters can conduct screening reviews"
- Review form hidden

---

### Scenario 6: Loop/Retry - Change Screening Decision

**Type:** 🔄 Loop/Retry

**Given**
- Candidate previously failed screening
- Hiring manager requests reconsideration

**When**
- I click "Revise Screening Decision"
- I change from Fail to Pass
- I add notes: "Manager approved based on portfolio review"

**Then**
- Status: Screening_Failed → Screening_Passed
- Audit log records decision reversal
- Candidate re-enters active pipeline

---

### Scenario 7: Empty State - No Candidates to Screen

**Type:** 📭 Empty State

**Given**
- All applications either not yet in Screening or already screened

**When**
- I navigate to "Screening Queue"

**Then**
- Empty state: "No candidates waiting for screening"
- Suggestion: "Check New candidates to start screening"

---

### Scenario 8: Session Timeout - Mid-Review

**Type:** ⏰ Timeout

**Given**
- Screening form open for 35 minutes
- Session expires (30 min timeout)

**When**
- I submit decision

**Then**
- Error: "Session expired"
- Notes preserved in localStorage
- After re-login: Form auto-restores with saved notes

---

### Scenario 9: Concurrent Modification - Candidate Withdrawn

**Type:** ⚡ Concurrent

**Given**
- I am reviewing candidate
- Candidate withdraws application during my review

**When**
- I submit screening decision

**Then**
- Error: "Candidate has withdrawn. Screening not saved."
- Application status already = Withdrew
- My review discarded

---

### Scenario 10: Data Integrity - Bulk Screening

**Type:** ⚠️ Data Integrity

**Given**
- 10 candidates in screening queue
- I use bulk review interface

**When**
- I mark 7 as Pass, 3 as Fail with reasons
- I submit bulk decision

**Then**
- All 10 updated atomically (transaction)
- If any fails validation: Entire batch rolled back
- Success: All 7 moved to Interview, 3 to Rejected

---

### Scenarios 11-20: Additional Coverage

11. **Alternative Path**: Phone screening vs. resume-only screening options
12. **Validation Error**: Screening notes too long (>2000 chars)
13. **Business Rule Error**: Cannot screen candidate in wrong status
14. **Permission Check**: HR Admin can override screening decisions
15. **Loop**: Re-screen after additional information provided
16. **Empty State**: Screening queue filtered shows no results
17. **Timeout**: Auto-save draft every 2 minutes
18. **Concurrent**: Two recruiters screen same candidate
19. **Integration Error**: Email notification fails (non-blocking)
20. **Performance**: Batch screen 50 candidates efficiently

---

## Scenario Coverage: ✅ Complete (20 scenarios, all 10 types)

---

## UI/UX Requirements

### Screening Review Form

```
╔═══════════════════════════════════════╗
║ Screening Review: Alex Chen           ║
╠═══════════════════════════════════════╣
║                                       ║
║ Fit Score: 92% (Excellent)            ║
║ Source: LinkedIn                      ║
║ Applied: 5 days ago                   ║
║                                       ║
║ Resume: [View PDF]                    ║
║                                       ║
║ Screening Decision:                   ║
║ ○ Pass - Move to Interview            ║
║ ○ Fail - Reject Candidate             ║
║                                       ║
║ Notes:                                ║
║ ┌───────────────────────────────────┐ ║
║ │ Strong technical background...    │ ║
║ │                                   │ ║
║ └───────────────────────────────────┘ ║
║                                       ║
║ [Save Draft] [Cancel] [Submit] ←     ║
╚═══════════════════════════════════════╝
```

**END OF US-4.6**
