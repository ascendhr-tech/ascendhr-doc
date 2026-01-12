# Schedule and Record Interview

**Story ID:** US-4.7  
**Epic:** Epic 0.7 - Scouting Network (ATS-Lite)  
**Persona:** Scout/Recruiter, Interviewer  
**Priority:** Must Have  
**Complexity:** M (2-3 days)

---

## User Story

> **As a** Scout/Recruiter,  
> **I want to** schedule interviews with assigned interviewers and track their status,  
> **So that** I can coordinate the interview process efficiently and ensure all stakeholders are informed.

---

## User Journey Context

### Entry Points
| Entry Source | Condition | User State |
|--------------|-----------|------------|
| Kanban board | Application in Interview stage | Ready to schedule |
| Application detail | Click "Schedule Interview" | Planning interview |
| Calendar integration | Available time slot selected | Coordinating schedules |

### Exit Points
| Exit Condition | Destination | User State |
|----------------|-------------|------------|
| Interview scheduled | Interview confirmation sent | Awaiting interview |
| Interview completed | Feedback collection (US-4.8) | Ready for decision |
| Interview cancelled | Application remains in queue | Need to reschedule |

---

## Business Logic

### Business Rules

| Rule ID | Description |
|---------|-------------|
| **BR-013** | Interview must have at least one interviewer assigned |
| **BR-007** | Multiple interviews allowed per application |

---

## Acceptance Criteria (20 Scenarios)

### Scenario 1: Happy Path - Schedule Single Interview

**Type:** ✅ Happy Path

**Given**
- Application in Interview_Scheduled status
- Interviewer "John Doe" available

**When**
- I click "Schedule Interview"
- I select interviewer: John Doe
- I pick date/time: 2026-03-15 14:00
- I set duration: 60 minutes
- I select type: "Technical Interview"
- I add meeting link: Zoom URL
- I click "Send Invites"

**Then**
- Interview record created with status = Scheduled
- Calendar invites sent to:
  - Candidate (external)
  - Interviewer John Doe
  - Recruiter (optional)
- Interview.scheduled_at = 2026-03-15 14:00
- Interview.interviewer_ids = [John Doe]
- Email confirmation sent to candidate
- Reminder scheduled 24 hours before
- Application.status remains Interview_Scheduled

---

### Scenario 2: Happy Path - Schedule Panel Interview

**Type:** ✅ Happy Path

**Given**
- Need multiple interviewers for senior role

**When**
- I select 3 interviewers: John Doe, Jane Smith, Mike Chen
- I schedule for 2026-03-15 14:00, 90 minutes
- I add agenda: "Technical skills (30min), System design (30min), Culture fit (30min)"

**Then**
- All 3 interviewers added to interview
- Calendar invites sent to all
- Agenda shared in meeting invite
- Interview.type = "Panel Interview"

---

### Scenario 3: Alternative Path - Multiple Interview Rounds

**Type:** 🔀 Alternative Path

**Given**
- Application requires 3 interview rounds

**When**
- I schedule:
  - Round 1: Phone screening (2026-03-10)
  - Round 2: Technical interview (2026-03-15)
  - Round 3: Final interview with manager (2026-03-20)

**Then**
- 3 separate Interview records created
- Each with status = Scheduled
- Application tracks: interviews_count = 3
- All rounds visible in timeline
- Can track completion per round

---

### Scenario 4: Alternative Path - Reschedule Interview

**Type:** 🔀 Alternative Path

**Given**
- Interview scheduled for 2026-03-15 14:00
- Interviewer has conflict

**When**
- I click "Reschedule"
- I change to 2026-03-16 10:00
- I add reason: "Interviewer conflict"

**Then**
- Interview.scheduled_at updated
- Updated calendar invites sent to all
- Email to candidate: "Your interview has been rescheduled..."
- Old time slot released
- Audit log: "Interview rescheduled from Mar 15 to Mar 16"

---

### Scenario 5: Alternative Path - Cancel Interview

**Type:** 🔀 Alternative Path

**Given**
- Interview scheduled
- Candidate withdraws application

**When**
- I click "Cancel Interview"
- I select reason: "Candidate withdrew"

**Then**
- Interview.status = Cancelled
- Calendar invites cancelled
- Notification sent to all participants
- Time slot freed
- Application.status updated appropriately

---

### Scenario 6: Validation Error - No Interviewer Assigned

**Type:** ❌ Validation Error (BR-013)

**Given**
- Scheduling interview form

**When**
- I set date/time but skip interviewer selection
- I click "Send Invites"

**Then**
- Error: "At least one interviewer must be assigned (BR-013)"
- Form not submitted
- Interviewer field highlighted

---

### Scenario 7: Validation Error - Past Date/Time

**Type:** ❌ Validation Error

**Given**
- Current date: 2026-03-15

**When**
- I select interview date: 2026-03-10 (past)

**Then**
- Error: "Interview cannot be scheduled in the past"
- Date picker shows error
- Suggestion: "Select a future date"

---

### Scenario 8: Validation Error - Interviewer Not Available

**Type:** ❌ Validation Error

**Given**
- Interviewer John Doe has meeting 14:00-15:00
- I try to schedule interview 14:30-15:30 (overlaps)

**When**
- System checks interviewer calendar
- Detects conflict

**Then**
- Warning: "John Doe has a conflict at this time"
- Show conflicting event details
- Suggest available times
- Allow override if urgent (with confirmation)

---

### Scenario 9: Business Rule Error - Duplicate Interview Same Time

**Type:** ⚠️ Business Rule Error

**Given**
- Interview already scheduled for 2026-03-15 14:00
- I create another interview same time

**When**
- System detects duplicate

**Then**
- Warning: "Interview already scheduled for this time"
- Options: "View existing" or "Schedule different time"

---

### Scenario 10: Permission Denied - Only Recruiters Schedule

**Type:** 🔒 Permission Denied

**Given**
- I am Interviewer (not Recruiter)

**When**
- I attempt to schedule interview

**Then**
- Error: "Only recruiters can schedule interviews"
- Form hidden
- Message: "Contact recruiter to schedule"

---

### Scenario 11: Loop/Retry - Edit Scheduled Interview

**Type:** 🔄 Loop/Retry

**Given**
- Interview scheduled
- Need to update meeting link

**When**
- I click "Edit Interview"
- I update Zoom link
- I click "Update & Notify"

**Then**
- Meeting link updated
- Updated invites sent
- No reschedule (time unchanged)

---

### Scenario 12: Empty State - No Interviews Scheduled

**Type:** 📭 Empty State

**Given**
- Application has no interviews yet

**When**
- I view interview section

**Then**
- Empty state: "No interviews scheduled"
- Button: "Schedule First Interview"

---

### Scenario 13: Session Timeout - Scheduling Form

**Type:** ⏰ Timeout

**Given**
- Form open for 35 minutes
- Session expires

**When**
- I submit schedule

**Then**
- Error: "Session expired"
- Form data preserved in localStorage
- After login: Auto-restore form

---

### Scenario 14: Concurrent Modification - Double-Book

**Type:** ⚡ Concurrent

**Given**
- Two recruiters scheduling with same interviewer
- Same time slot

**When**
- Both submit simultaneously

**Then**
- First request succeeds
- Second request: "Time slot just booked"
- Suggest alternative times

---

### Scenario 15: Integration Error - Calendar API Down

**Type:** ⚠️ Integration Error

**Given**
- Google Calendar API unavailable

**When**
- I schedule interview

**Then**
- Interview record created (success)
- Warning: "Calendar invites will be sent when service available"
- Queued for retry
- Core functionality not blocked

---

### Scenario 16: Alternative Path - Video Conference Auto-Create

**Type:** 🔀 Alternative Path

**Given**
- Scheduling remote interview

**When**
- I select "Create video meeting"

**Then**
- Zoom/Google Meet link auto-generated
- Link added to interview record
- Link included in invites
- No manual link creation needed

---

### Scenario 17: Alternative Path - Template Interview Types

**Type:** 🔀 Alternative Path

**Given**
- Common interview types configured

**When**
- I select from templates:
  - "Phone Screening" (30min)
  - "Technical Interview" (60min)
  - "Culture Fit" (45min)
  - "Final Interview" (90min)

**Then**
- Duration auto-filled
- Suggested questions loaded
- Standard agenda pre-populated

---

### Scenario 18: Loop/Retry - Send Reminder

**Type:** 🔄 Loop/Retry

**Given**
- Interview tomorrow
- Auto-reminder sent
- Candidate didn't confirm

**When**
- I click "Send Manual Reminder"

**Then**
- Additional reminder sent
- Log: "Manual reminder sent"

---

### Scenario 19: Data Integrity - Interview History

**Type:** ⚠️ Data Integrity

**Given**
- Multiple rescheduling events

**When**
- I view interview history

**Then**
- All versions tracked:
  - Original: Mar 15 14:00 (rescheduled)
  - Revised: Mar 16 10:00 (rescheduled)
  - Final: Mar 17 15:00 (completed)
- Audit trail complete

---

### Scenario 20: Performance - Bulk Schedule

**Type:** ⚠️ Performance

**Given**
- Need to schedule 20 interviews

**When**
- I use bulk scheduling tool

**Then**
- All 20 scheduled within 30 seconds
- Calendar invites batched
- No timeout or performance issues

---

## Scenario Coverage: ✅ Complete (20 scenarios, all 10 types)

---

## UI/UX Requirements

### Interview Scheduling Form

```
╔═══════════════════════════════════════╗
║ Schedule Interview                    ║
╠═══════════════════════════════════════╣
║ Candidate: Alex Chen                  ║
║ Position: Senior Backend Developer    ║
║                                       ║
║ Interview Type:                       ║
║ [Technical Interview ▼]               ║
║                                       ║
║ Date & Time:                          ║
║ [2026-03-15 ▼] [14:00 ▼]             ║
║                                       ║
║ Duration:                             ║
║ [60 minutes ▼]                        ║
║                                       ║
║ Interviewers: *                       ║
║ [+ John Doe] [+ Jane Smith]           ║
║                                       ║
║ Meeting Link:                         ║
║ [Auto-generate Zoom ▼]                ║
║ https://zoom.us/j/123...              ║
║                                       ║
║ Agenda (optional):                    ║
║ ┌───────────────────────────────────┐ ║
║ │ Technical skills assessment...    │ ║
║ └───────────────────────────────────┘ ║
║                                       ║
║ [Cancel] [Save Draft] [Send Invites] ║
╚═══════════════════════════════════════╝
```

**END OF US-4.7**
