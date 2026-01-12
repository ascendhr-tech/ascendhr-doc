# Collect Interview Feedback

**Story ID:** US-4.8  
**Epic:** Epic 0.7 - Scouting Network (ATS-Lite)  
**Persona:** Interviewer, Scout/Recruiter  
**Priority:** Must Have  
**Complexity:** M (2 days)

---

## User Story

> **As an** Interviewer,  
> **I want to** submit structured feedback after conducting an interview,  
> **So that** hiring decisions are based on consistent, documented evaluations.

---

## User Journey Context

### Entry Points
| Entry Source | Condition | User State |
|--------------|-----------|------------|
| Email reminder | "Submit feedback for Alex Chen interview" | Post-interview |
| Interview calendar | After meeting ends, notification | Fresh impressions |
| Application page | Click "Add Feedback" | Reviewing candidate |

### Exit Points
| Exit Condition | Destination | User State |
|----------------|-------------|------------|
| Feedback submitted | Application dashboard | Task complete |
| Strong positive | Recruiter notified to move to Offer | Excited about candidate |
| Negative feedback | Application flagged for rejection | Clear decision |

---

## Business Logic

### Business Rules

| Rule ID | Description |
|---------|-------------|
| **BR-016** | Interview feedback required before moving to Offer stage |
| **BR-017** | Feedback includes rating (1-5) and detailed comments |

---

## Acceptance Criteria (20 Scenarios)

### Scenario 1: Happy Path - Submit Positive Feedback

**Type:** ✅ Happy Path

**Given**
- I am Interviewer John Doe
- Just completed technical interview with Alex Chen
- Interview.status = Completed

**When**
- I click "Submit Feedback" from email link
- Feedback form opens pre-filled with:
  - Candidate: Alex Chen
  - Interview Type: Technical Interview
  - Date: 2026-03-15 14:00
- I select overall rating: ⭐⭐⭐⭐⭐ (5/5 - Strong Hire)
- I rate technical skills:
  - Coding: 5/5
  - Problem Solving: 5/5
  - System Design: 4/5
  - Communication: 5/5
- I add detailed comments:
  ```
  Excellent technical skills. Solved complex algorithm
  problem efficiently. Great communication and culture fit.
  Strong recommendation to hire.
  ```
- I select recommendation: "Strong Hire"
- I click "Submit Feedback"

**Then**
- Feedback record created with:
  - interview_id linked
  - interviewer_id = John Doe
  - overall_rating = 5
  - recommendation = "Strong Hire"
  - comments saved
  - submitted_at = current timestamp
- Interview.status = Feedback_Submitted
- Interview.feedback_count = 1
- Recruiter notified: "John Doe submitted positive feedback for Alex Chen"
- Application flagged for offer consideration
- Feedback visible to recruiter and hiring manager
- Feedback NOT visible to candidate (internal only)

---

### Scenario 2: Happy Path - Submit Negative Feedback

**Type:** ✅ Happy Path

**Given**
- Interview completed
- Candidate struggled with technical questions

**When**
- I rate overall: ⭐⭐ (2/5 - Not Recommended)
- I rate skills:
  - Coding: 2/5
  - Problem Solving: 3/5
  - System Design: 2/5
  - Communication: 4/5
- I add comments:
  ```
  Candidate showed good soft skills but lacked
  technical depth. Unable to solve basic algorithm
  problems. Not recommended for senior role.
  ```
- I select recommendation: "No Hire"
- I submit

**Then**
- Feedback saved
- Recruiter alerted: "Negative feedback received"
- Application flagged for rejection
- Suggestion to recruiter: "Consider rejecting or additional technical screening"

---

### Scenario 3: Alternative Path - Mixed Feedback (Panel Interview)

**Type:** 🔀 Alternative Path

**Given**
- Panel interview with 3 interviewers
- Each submits separate feedback

**When**
- Interviewer 1: Rating 5/5, "Strong Hire"
- Interviewer 2: Rating 3/5, "Maybe"
- Interviewer 3: Rating 4/5, "Hire"

**Then**
- All 3 feedback records linked to same interview
- Average rating calculated: (5+3+4)/3 = 4.0
- Interview.average_rating = 4.0
- Recruiter sees all 3 individual feedback
- Summary: "2 Hire, 1 Maybe - Proceed with offer"
- Hiring manager reviews discrepancy

---

### Scenario 4: Alternative Path - Save Draft Feedback

**Type:** 🔀 Alternative Path

**Given**
- Started feedback form
- Need to check notes before submitting

**When**
- I fill partial feedback
- I click "Save Draft"

**Then**
- Feedback saved with status = Draft
- Not visible to recruiter yet
- Reminder sent: "Complete feedback for Alex Chen"
- Can resume later with pre-filled data

---

### Scenario 5: Alternative Path - Edit Submitted Feedback

**Type:** 🔀 Alternative Path

**Given**
- Submitted feedback yesterday
- Realized I rated System Design incorrectly

**When**
- I click "Edit Feedback" (within 48 hours)
- I change System Design: 3/5 → 4/5
- I update comments
- I click "Update Feedback"

**Then**
- Feedback updated
- Version history maintained
- Audit log: "Feedback edited by John Doe"
- Recruiter notified of update
- After 48 hours: Feedback locked (cannot edit)

---

### Scenario 6: Validation Error - Missing Required Rating

**Type:** ❌ Validation Error (BR-017)

**Given**
- Feedback form open

**When**
- I add comments but skip overall rating
- I click "Submit"

**Then**
- Error: "Overall rating is required (BR-017)"
- Rating field highlighted
- Form not submitted

---

### Scenario 7: Validation Error - Comments Too Short

**Type:** ❌ Validation Error

**Given**
- Feedback form

**When**
- I rate 2/5 but only type "Not good"
- Comments < 20 characters

**Then**
- Error: "Please provide detailed feedback (minimum 20 characters)"
- Comments field highlighted
- Suggestion: "Explain your rating to help hiring decision"

---

### Scenario 8: Business Rule Error - Submit Before Interview

**Type:** ⚠️ Business Rule Error

**Given**
- Interview scheduled for tomorrow
- I try to submit feedback early

**When**
- I access feedback form

**Then**
- Error: "Cannot submit feedback before interview is completed"
- Form disabled
- Message: "Interview is scheduled for Mar 15, 2026"

---

### Scenario 9: Business Rule Error - Cannot Move to Offer Without Feedback

**Type:** ⚠️ Business Rule Error (BR-016)

**Given**
- Interview completed
- No feedback submitted yet
- Recruiter tries to move to Offer stage

**When**
- Recruiter drags application to Offer column

**Then**
- Error: "Cannot move to Offer: Interview feedback required (BR-016)"
- Card snaps back
- Message to recruiter: "Request feedback from interviewer John Doe"
- Link to send reminder

---

### Scenario 10: Permission Denied - Candidate Cannot View Feedback

**Type:** 🔒 Permission Denied

**Given**
- Candidate tries to access feedback

**When**
- Candidate navigates to feedback URL

**Then**
- Error: "Access Denied: Feedback is internal only"
- No feedback details shown
- Candidate sees only: "Interview completed - awaiting decision"

---

### Scenario 11: Loop/Retry - Remind Interviewer

**Type:** 🔄 Loop/Retry

**Given**
- Interview completed 3 days ago
- No feedback submitted
- Recruiter needs decision

**When**
- Recruiter clicks "Send Reminder"

**Then**
- Email to interviewer: "Reminder: Submit feedback for Alex Chen"
- Link to feedback form
- Shows time elapsed: "Interview was 3 days ago"
- Escalation after 5 days: Notify hiring manager

---

### Scenario 12: Empty State - No Feedback Yet

**Type:** 📭 Empty State

**Given**
- Interview completed
- Viewing interview details

**When**
- Recruiter checks feedback section

**Then**
- Empty state: "No feedback submitted yet"
- Interviewer name: "Waiting for John Doe"
- Button: "Send Reminder"
- Status: "Pending feedback"

---

### Scenario 13: Session Timeout - Feedback Form

**Type:** ⏰ Timeout

**Given**
- Feedback form open for 40 minutes
- Session expires

**When**
- I submit feedback

**Then**
- Error: "Session expired"
- Feedback preserved in localStorage
- After login: Auto-restore form
- No data loss

---

### Scenario 14: Concurrent Modification - Duplicate Feedback

**Type:** ⚡ Concurrent

**Given**
- I open feedback form in 2 browser tabs
- Submit from both tabs

**When**
- Both submissions hit server

**Then**
- First submission: Success
- Second submission: Error "Feedback already submitted"
- Show existing feedback
- Option to edit instead

---

### Scenario 15: Integration Error - Email Notification Failed

**Type:** ⚠️ Integration Error

**Given**
- Feedback submitted
- Email service down

**When**
- System tries to notify recruiter

**Then**
- Feedback saved successfully (core function)
- Warning: "Email notification failed - will retry"
- Queued for retry
- In-app notification still shown
- Not blocking

---

### Scenario 16: Alternative Path - Quick Feedback Template

**Type:** 🔀 Alternative Path

**Given**
- Common feedback patterns

**When**
- I select template: "Strong technical skills, recommended"

**Then**
- Pre-filled comments:
  ```
  Demonstrated strong technical skills.
  Good problem-solving approach.
  Clear communication.
  Recommend to hire.
  ```
- I can customize before submitting
- Saves time for common scenarios

---

### Scenario 17: Alternative Path - Anonymous Feedback Option

**Type:** 🔀 Alternative Path

**Given**
- Sensitive feedback about culture fit

**When**
- I check "Submit as anonymous"
- I provide honest concerns

**Then**
- Feedback.is_anonymous = true
- Recruiter sees feedback without interviewer name
- Encourages honest evaluation
- Audit trail still tracks (for admin only)

---

### Scenario 18: Loop/Retry - Request Additional Feedback

**Type:** 🔄 Loop/Retry

**Given**
- First interviewer: 5/5 Strong Hire
- Hiring manager uncertain

**When**
- Manager requests second opinion
- Schedule second interview with different interviewer

**Then**
- Second interview created
- Second feedback collected
- Both feedback visible
- Decision based on combined input

---

### Scenario 19: Data Integrity - Aggregate Panel Feedback

**Type:** ⚠️ Data Integrity

**Given**
- 4 interviewers in panel
- All submit feedback

**When**
- System aggregates ratings

**Then**
- Calculate average across all dimensions
- Identify outliers (e.g., 1 person rated 2/5, others 5/5)
- Flag discrepancies for review
- Show consensus vs. dissenting opinions
- Help hiring manager make informed decision

---

### Scenario 20: Performance - Bulk Feedback Collection

**Type:** ⚠️ Performance

**Given**
- 10 interviews completed in one day
- Each interviewer has multiple feedback to submit

**When**
- I use batch feedback interface

**Then**
- All 10 feedback forms accessible
- Save drafts independently
- Submit in batch
- No performance lag
- Progress indicator: "3 of 10 completed"

---

## Scenario Coverage: ✅ Complete (20 scenarios, all 10 types)

---

## UI/UX Requirements

### Feedback Form

```
╔═══════════════════════════════════════╗
║ Interview Feedback                    ║
╠═══════════════════════════════════════╣
║ Candidate: Alex Chen                  ║
║ Interview: Technical Interview        ║
║ Date: March 15, 2026                  ║
║                                       ║
║ Overall Recommendation: *             ║
║ ○ Strong Hire (5)                     ║
║ ○ Hire (4)                            ║
║ ○ Maybe (3)                           ║
║ ○ No Hire (2)                         ║
║ ○ Strong No Hire (1)                  ║
║                                       ║
║ Technical Skills:                     ║
║ Coding:          ⭐⭐⭐⭐⭐            ║
║ Problem Solving: ⭐⭐⭐⭐⭐            ║
║ System Design:   ⭐⭐⭐⭐☆            ║
║ Communication:   ⭐⭐⭐⭐⭐            ║
║                                       ║
║ Detailed Comments: *                  ║
║ ┌───────────────────────────────────┐ ║
║ │ Excellent technical skills...     │ ║
║ │                                   │ ║
║ │                                   │ ║
║ └───────────────────────────────────┘ ║
║                                       ║
║ ☐ Submit as anonymous                 ║
║                                       ║
║ [Save Draft] [Cancel] [Submit] ←     ║
╚═══════════════════════════════════════╝
```

### Feedback Summary View (for Recruiter)

```
╔═══════════════════════════════════════╗
║ Interview Feedback Summary            ║
╠═══════════════════════════════════════╣
║ Panel Interview - 3 Interviewers      ║
║                                       ║
║ Overall: 4.0/5.0 (Recommended)        ║
║                                       ║
║ John Doe (Tech Lead)                  ║
║ ⭐⭐⭐⭐⭐ Strong Hire                 ║
║ "Excellent technical depth..."        ║
║                                       ║
║ Jane Smith (Senior Dev)               ║
║ ⭐⭐⭐☆☆ Maybe                        ║
║ "Good but lacks experience in..."     ║
║                                       ║
║ Mike Chen (Manager)                   ║
║ ⭐⭐⭐⭐☆ Hire                        ║
║ "Strong culture fit, recommend..."    ║
║                                       ║
║ Consensus: Proceed with Offer         ║
║                                       ║
║ [View Details] [Move to Offer]        ║
╚═══════════════════════════════════════╝
```

**END OF US-4.8**
