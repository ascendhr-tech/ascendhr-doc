# Send Email Notifications to Candidates

**Story ID:** US-4.13  
**Epic:** Epic 0.7 - Scouting Network (ATS-Lite)  
**Persona:** Scout/Recruiter, System  
**Priority:** Nice to Have  
**Complexity:** S (1-2 days)

---

## User Story

> **As a** Scout/Recruiter,  
> **I want to** automatically send email notifications to candidates at key pipeline stages,  
> **So that** candidates stay informed and engaged throughout the recruitment process.

---

## User Journey Context

### Entry Points
| Entry Source | Condition | User State |
|--------------|-----------|------------|
| Application status change | Auto-trigger | System automated |
| Manual send | Recruiter clicks "Send Update" | Proactive communication |
| Template configuration | Setup email templates | Initial configuration |

### Exit Points
| Exit Condition | Destination | User State |
|----------------|-------------|------------|
| Email sent | Email in candidate inbox | Candidate informed |
| Email failed | Retry queue | System handles retry |
| Candidate replies | Recruiter inbox | Follow-up needed |

---

## Business Logic

### Email Triggers

| Trigger Event | Email Type | Auto/Manual | Content |
|---------------|------------|-------------|---------|
| Application received | Confirmation | Auto | "We received your application" |
| Moved to Interview | Interview invite | Auto | Interview details + calendar |
| Interview completed | Thank you | Auto (optional) | "Thank you for interviewing" |
| Offer sent | Offer letter | Manual | Offer details + accept/reject links |
| Offer accepted | Welcome | Auto | "Welcome to the team" |
| Application rejected | Rejection | Manual | Polite rejection with feedback |

---

## Acceptance Criteria (20 Scenarios)

### Scenario 1: Happy Path - Application Received Confirmation

**Type:** ✅ Happy Path

**Given**
- Candidate "Alex Chen" submits application
- Application created successfully
- Auto-confirmation enabled

**When**
- Application status = New

**Then**
- Email sent to alex.chen@email.com within 1 minute
- Subject: "Application Received - Senior Backend Developer at AscendHR"
- Body includes:
  ```
  Hi Alex,
  
  Thank you for applying to the Senior Backend Developer position.
  We've received your application and our team will review it shortly.
  
  What happens next:
  - Our team will review your application (2-3 business days)
  - If shortlisted, we'll contact you for an interview
  
  Application ID: APP-2026-050
  Position: Senior Backend Developer
  
  Best regards,
  AscendHR Recruitment Team
  ```
- Email delivery status logged
- Candidate receives email in inbox

---

### Scenario 2: Happy Path - Interview Invitation

**Type:** ✅ Happy Path

**Given**
- Interview scheduled for 2026-03-15 14:00
- Interviewer: John Doe
- Meeting link: Zoom URL

**When**
- Interview created and confirmed

**Then**
- Email sent to candidate
- Subject: "Interview Invitation - Senior Backend Developer"
- Body includes:
  ```
  Hi Alex,
  
  Great news! We'd like to invite you for an interview.
  
  Interview Details:
  - Date: Friday, March 15, 2026
  - Time: 2:00 PM (GMT+7)
  - Duration: 60 minutes
  - Interviewer: John Doe, Tech Lead
  - Type: Technical Interview
  
  Join Meeting: [Zoom Link]
  Add to Calendar: [.ics attachment]
  
  Preparation:
  - Review the job description
  - Prepare questions about the role
  - Test your camera/microphone
  
  Need to reschedule? Reply to this email.
  
  Best regards,
  AscendHR Team
  ```
- Calendar invite (.ics) attached
- Zoom link clickable
- Professional formatting

---

### Scenario 3: Happy Path - Rejection Email

**Type:** ✅ Happy Path

**Given**
- Application rejected after screening
- Rejection reason: "Insufficient experience"

**When**
- Recruiter clicks "Send Rejection Email"
- Selects template: "Polite Rejection"

**Then**
- Email sent
- Subject: "Update on Your Application"
- Body (professional, respectful):
  ```
  Hi Alex,
  
  Thank you for your interest in the Senior Backend Developer
  position at AscendHR.
  
  After careful review, we've decided to move forward with
  other candidates whose experience more closely matches
  our current needs.
  
  We appreciate the time you invested in the application
  process. We encourage you to apply for future positions
  that match your skills.
  
  We wish you success in your job search.
  
  Best regards,
  AscendHR Recruitment Team
  ```
- Tone: Respectful, brief, no detailed reasons
- No "Unfortunately" (avoid negative words)
- Encourages future applications

---

### Scenario 4: Alternative Path - Custom Message

**Type:** 🔀 Alternative Path

**Given**
- Need to send custom message to candidate
- Not a standard template situation

**When**
- Recruiter clicks "Send Custom Email"
- Writes personalized message:
  ```
  Hi Alex,
  
  Thanks for the great interview yesterday. The team was
  impressed with your portfolio. We'd like to schedule a
  follow-up session to discuss the React project you mentioned.
  
  Are you available next Tuesday?
  ```
- Sends

**Then**
- Custom email sent (not from template)
- Logged in communication history
- Candidate can reply directly

---

### Scenario 5: Alternative Path - Bulk Email to Multiple Candidates

**Type:** 🔀 Alternative Path

**Given**
- 10 candidates passed screening
- Need to invite all for interview prep webinar

**When**
- Recruiter selects 10 candidates
- Clicks "Send Bulk Email"
- Selects template: "Webinar Invitation"
- Personalizes: "Join our interview prep webinar on Friday"

**Then**
- 10 emails queued
- Each personalized with candidate name
- BCC to all (privacy - candidates don't see each other)
- Sent in batch within 5 minutes
- Delivery status tracked per candidate

---

### Scenario 6: Validation Error - Invalid Email Address

**Type:** ❌ Validation Error

**Given**
- Candidate email: "invalid-email" (malformed)

**When**
- System attempts to send confirmation email

**Then**
- Email validation fails
- Error logged: "Invalid email address for candidate CAN-2026-010"
- Alert to recruiter: "Cannot send email - invalid address"
- Candidate record flagged for review
- Recruiter must update email manually

---

### Scenario 7: Validation Error - Missing Email Template

**Type:** ❌ Validation Error

**Given**
- Trigger: Application rejected
- Email template "Rejection" not configured

**When**
- System attempts to send email

**Then**
- Error: "Email template 'Rejection' not found"
- Email not sent
- Alert to admin: "Configure missing template"
- Fallback: Generic rejection template used

---

### Scenario 8: Business Rule Error - Email Daily Limit Exceeded

**Type:** ⚠️ Business Rule Error

**Given**
- Email service has limit: 100 emails/day
- Already sent 95 emails today
- Attempting to send 10 more

**When**
- Bulk send triggered

**Then**
- First 5 emails sent (total 100)
- Remaining 5 queued for tomorrow
- Warning: "Email limit reached - 5 emails queued for next day"
- Ensures compliance with provider limits

---

### Scenario 9: Business Rule Error - Candidate Unsubscribed

**Type:** ⚠️ Business Rule Error

**Given**
- Candidate previously clicked "Unsubscribe" link
- Candidate.email_notifications = false

**When**
- System attempts to send update

**Then**
- Email blocked (respect unsubscribe)
- Log: "Email not sent - candidate unsubscribed"
- Only send critical emails (offer, interview cancellation)
- Non-critical updates skipped

---

### Scenario 10: Permission Denied - Only Recruiters Send Manual Emails

**Type:** 🔒 Permission Denied

**Given**
- I am Interviewer (not Recruiter)

**When**
- I attempt to send email to candidate

**Then**
- Error: "Only recruiters can send emails to candidates"
- Email compose button hidden
- Suggestion: "Contact recruiter to send message"

---

### Scenario 11: Loop/Retry - Resend Failed Email

**Type:** 🔄 Loop/Retry

**Given**
- Email sent but delivery failed (bounce)
- Email service returned error: "Mailbox full"

**When**
- Recruiter clicks "Retry Send"

**Then**
- Email re-queued
- Retry after 1 hour
- If fails again: Try alternate email (if available)
- After 3 failures: Alert recruiter to contact candidate by phone

---

### Scenario 12: Empty State - No Email History

**Type:** 📭 Empty State

**Given**
- Candidate just added
- No emails sent yet

**When**
- View email history for candidate

**Then**
- Empty state: "No emails sent yet"
- Suggestion: "Send introduction email"
- Template quick-actions shown

---

### Scenario 13: Session Timeout - Composing Email

**Type:** ⏰ Timeout

**Given**
- Composing custom email for 40 minutes
- Session expires

**When**
- Click "Send"

**Then**
- Error: "Session expired"
- Email draft saved in localStorage
- After re-login: Draft auto-restored
- Can send without rewriting

---

### Scenario 14: Concurrent Modification - Duplicate Email Send

**Type:** ⚡ Concurrent

**Given**
- Two recruiters viewing same application
- Both click "Send Interview Invite" simultaneously

**When**
- Both requests hit server

**Then**
- First request: Email sent
- Second request: Blocked with error "Email already sent 10 seconds ago"
- Prevents duplicate emails to candidate
- Deduplication based on email type + candidate + time window

---

### Scenario 15: Integration Error - Email Service Down

**Type:** ⚠️ Integration Error

**Given**
- SendGrid/SES API unavailable (503 error)

**When**
- Attempting to send confirmation email

**Then**
- Email queued in outbox
- Status: "Pending - service unavailable"
- Retry every 10 minutes (max 24 hours)
- Alert admin if service down >1 hour
- Core application continues working (non-blocking)

---

### Scenario 16: Alternative Path - Schedule Email for Later

**Type:** 🔀 Alternative Path

**Given**
- Want to send rejection email
- But timing is bad (Friday evening)

**When**
- Recruiter clicks "Schedule Send"
- Selects: Monday 9:00 AM

**Then**
- Email queued with scheduled_send_at
- Not sent immediately
- Sent automatically Monday 9 AM
- Can cancel scheduled email before send time

---

### Scenario 17: Alternative Path - Email Preview Before Send

**Type:** 🔀 Alternative Path

**Given**
- About to send offer email
- Want to verify content first

**When**
- Click "Preview Email"

**Then**
- Modal shows rendered email:
  - Subject line
  - Full body with merged variables
  - Attachments listed
  - "Test Send to Me" option
- Can edit before final send

---

### Scenario 18: Loop/Retry - Update Email Template

**Type:** 🔄 Loop/Retry

**Given**
- Rejection email template has typo
- Already sent to 5 candidates

**When**
- Admin fixes template typo
- Saves updated template

**Then**
- Future emails use corrected template
- Past emails unchanged (already sent)
- Audit log: "Template updated by admin"

---

### Scenario 19: Data Integrity - Email Tracking

**Type:** ⚠️ Data Integrity

**Given**
- Email sent to candidate

**When**
- Tracking delivery status

**Then**
- Email record includes:
  - sent_at: 2026-03-15 10:00:00
  - status: Delivered (or Bounced, Opened, Clicked)
  - message_id: unique ID from email service
  - opens_count: 2 (if tracking enabled)
  - clicked_links: ["Zoom link", "Calendar"] (if tracking enabled)
- Full audit trail for compliance

---

### Scenario 20: Performance - Send 100 Emails Efficiently

**Type:** ⚠️ Performance

**Given**
- 100 candidates rejected (position filled)
- Need to send rejection emails to all

**When**
- Bulk send rejection emails

**Then**
- Emails processed in batches of 20
- All 100 sent within 10 minutes
- No timeouts or failures
- Progress indicator: "Sending... 60/100"
- Success summary: "100 emails sent successfully"

---

## Scenario Coverage: ✅ Complete (20 scenarios, all 10 types)

---

## UI/UX Requirements

### Email Composer

```
╔═══════════════════════════════════════╗
║ Send Email to Candidate               ║
╠═══════════════════════════════════════╣
║ To: alex.chen@email.com               ║
║                                       ║
║ Template: [Interview Invitation ▼]    ║
║                                       ║
║ Subject:                              ║
║ Interview Invitation - Senior Backend ║
║                                       ║
║ Body:                                 ║
║ ┌───────────────────────────────────┐ ║
║ │ Hi Alex,                          │ ║
║ │                                   │ ║
║ │ We'd like to invite you for...   │ ║
║ │                                   │ ║
║ │ [Template variables merged]       │ ║
║ └───────────────────────────────────┘ ║
║                                       ║
║ Attachments:                          ║
║ [+ Add File] interview_prep.pdf       ║
║                                       ║
║ ☐ Schedule send for later             ║
║                                       ║
║ [Preview] [Save Draft] [Send] ←      ║
╚═══════════════════════════════════════╝
```

### Email History View

```
╔═══════════════════════════════════════╗
║ Email History: Alex Chen              ║
╠═══════════════════════════════════════╣
║                                       ║
║ Mar 15, 2026 10:00 AM                 ║
║ ✉️ Application Received                ║
║ Status: Delivered ✓                   ║
║ Opened: 2 times                       ║
║                                       ║
║ Mar 16, 2026 2:30 PM                  ║
║ ✉️ Interview Invitation                ║
║ Status: Delivered ✓                   ║
║ Opened: 5 times                       ║
║ Clicked: Zoom link, Calendar          ║
║                                       ║
║ Mar 20, 2026 9:00 AM                  ║
║ ✉️ Thank You - Interview               ║
║ Status: Sent ⏱️                        ║
║                                       ║
║ [Send New Email]                      ║
╚═══════════════════════════════════════╝
```

### Template Management

```
╔═══════════════════════════════════════╗
║ Email Templates                       ║
╠═══════════════════════════════════════╣
║                                       ║
║ Application Received    [Edit] [Test] ║
║ Interview Invitation    [Edit] [Test] ║
║ Rejection (Polite)      [Edit] [Test] ║
║ Offer Letter            [Edit] [Test] ║
║ Welcome Email           [Edit] [Test] ║
║                                       ║
║ [+ Create New Template]               ║
║                                       ║
║ Variables Available:                  ║
║ {{candidate_name}}                    ║
║ {{position_title}}                    ║
║ {{interview_date}}                    ║
║ {{interview_time}}                    ║
║ {{recruiter_name}}                    ║
╚═══════════════════════════════════════╝
```

**END OF US-4.13**
