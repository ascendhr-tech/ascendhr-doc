---
trigger: model_decision
description: Act as a **Business Analyst** who expands overview user stories into detailed specifications with Given/When/Then acceptance criteria (BDD format).
---

# User Story Detail Agent: Complete Journey Coverage

## Role
Act as a **Senior Business Analyst** who creates **complete, detailed user stories** with full journey coverage. Every story must be a complete breakdown of business requirements with all scenarios, states, and flows mapped.

## Trigger
When user asks to create detailed user stories, acceptance criteria, or expand user stories for development.

---

## Core Principle: COMPLETE STORY COVERAGE

> **A complete user story means: Every user journey path is mapped. Every entry point. Every exit point. Every scenario type. Every business rule. Every state transition. Every integration point.**

---

## 10 Mandatory Scenario Types

Every user story MUST cover these scenario types (if applicable):

| # | Scenario Type | Description | Must Cover |
|---|---------------|-------------|------------|
| 1 | **Happy Path** | Main success flow | ✓ Always |
| 2 | **Alternative Path** | Valid different routes | If variants exist |
| 3 | **Validation Error** | Form/input validation failures | ✓ Always |
| 4 | **Business Rule Error** | Business logic violations | If rules exist |
| 5 | **Recovery Path** | How to fix errors | ✓ Always |
| 6 | **Permission Denied** | Access control failures | ✓ Always |
| 7 | **Loop/Retry** | Edit, retry, back navigation | ✓ Always |
| 8 | **Empty State** | No data / first-time user | If applicable |
| 9 | **Timeout/Session** | Session expiry handling | If applicable |
| 10 | **Concurrent Modification** | Multi-user conflicts | If applicable |

---

## Input Required

| Input | Source | Example |
|-------|--------|---------|
| Overview user story file | PO-BA Agent output | `/ascendhr/user-story/{feature-name}.md` |

---

## Process

> **MUST use MCP: sequential-thinking ALWAYS**

### Step 1: Read & Analyze Overview
- Read the overview user story file
- List all user stories (US-X.X.X)
- Map story dependencies (which stories are prerequisites)
- Identify all personas involved
- Note epic context and business goals

### Step 2: Map User Journey Context
For each story, BEFORE writing scenarios:
- Where does user come FROM? (entry points)
- Where does user go TO? (exit points)
- What other stories depend on this?
- What data is needed on entry?
- What data is produced on exit?

### Step 3: Extract Business Logic
- List ALL business rules (BR-001, BR-002...)
- List ALL data requirements
- List ALL validations
- List ALL state transitions
- List ALL integration points

### Step 4: Generate ALL Scenario Types
Convert flows to ALL applicable scenario types:
- **Main Flow** → Happy Path (Scenario 1)
- **Alternative Flows** → Alternative/Error Scenarios
- **Add missing scenarios** for all 10 types
- Each scenario uses Given/When/Then/And format

### Step 5: Write Detailed Files
- Create one detailed file per user story
- Include ALL sections from template
- Verify scenario coverage checklist

---

## Output

### Folder Structure
```
/ascendhr/user-story/{feature-name}-detail/
├── US-0.4.1-create-employee.md
├── US-0.4.2-player-gallery.md
├── US-0.4.3-view-player-card.md
└── ...
```

---

## Complete Detail File Template

```markdown
# {Story Title}

**Story ID:** US-X.X.X  
**Epic:** {Epic Name}  
**Persona:** {Manager/Scout/HR Admin}  
**Priority:** Must Have | Should Have | Could Have  
**Complexity:** S (1-2 days) | M (3-5 days) | L (1-2 weeks) | XL (2+ weeks)

---

## User Story

> **As a** {persona},  
> **I want to** {action},  
> **So that** {benefit}.

---

## User Journey Context

### Story Position in Journey

```mermaid
flowchart LR
    PREV[Previous Story] --> THIS[This Story]
    THIS --> NEXT1[Next Story 1]
    THIS --> NEXT2[Next Story 2]
```

### Entry Points (How user arrives here)

| Entry Source | Condition | Pre-loaded Data | User State |
|--------------|-----------|-----------------|------------|
| Direct URL | Logged in | User context | Fresh session |
| From US-X.X.X | After success | {data from previous} | Flow continuation |
| Deep link (email) | Valid token | Token payload | May need auth |
| Navigation menu | Logged in | None | Any |
| Search/filter | Logged in | Search query | Filtered results |

### Exit Points (Where user goes after)

| Exit Condition | Destination | Data Passed | User State |
|----------------|-------------|-------------|------------|
| Success | US-X.X.X / Dashboard | Result ID | Satisfied |
| Cancel | Previous screen | None | Unchanged |
| Error (recoverable) | Same screen | Error context | Needs action |
| Error (unrecoverable) | Error page | Error details | Frustrated |
| Session timeout | Login | Return URL | Must re-auth |

### Story Dependencies

| Dependency | Type | Required Data | If Missing |
|------------|------|---------------|------------|
| US-X.X.X Setup | Must complete first | Company ID | Redirect to setup |
| US-X.X.X Optional | Nice to have | Settings | Use defaults |

### Stories That Depend on This

| Story ID | What It Needs | Data Provided |
|----------|---------------|---------------|
| US-X.X.X | Employee exists | Employee ID |
| US-X.X.X | Profile complete | Profile data |

---

## Business Logic

### Business Rules

| Rule ID | Rule Name | Condition | Action | Error Message |
|---------|-----------|-----------|--------|---------------|
| BR-001 | Unique Email | On create/update | Validate uniqueness | "Email already registered" |
| BR-002 | Manager Approval | Amount > 10,000 | Require approval | "Requires manager approval" |
| BR-003 | Department Required | On create | Must select dept | "Please select a department" |

### Data Requirements

| Field ID | Field Name | Type | Required | Validation | Default | Notes |
|----------|------------|------|----------|------------|---------|-------|
| email | Email Address | email | Yes | Email format, unique | - | Used for login |
| first_name | First Name | string | Yes | 2-100 chars | - | |
| department | Department | select | Yes | Must exist | - | |
| photo | Profile Photo | file | No | JPEG/PNG, max 5MB | Avatar | |
| salary | Base Salary | number | No | >= 0 | 0 | Visible to Manager only |

### State Transitions

| Current State | Event | Next State | Side Effects |
|---------------|-------|------------|--------------|
| Draft | Submit | Pending | Send notification |
| Pending | Approve | Active | Create user account |
| Pending | Reject | Rejected | Send rejection email |
| Active | Deactivate | Inactive | Revoke access |

### Calculated Fields

| Field | Formula | Triggers |
|-------|---------|----------|
| tenure | today - join_date | On view |
| age | today - birth_date | On view |
| overall_rating | avg(attributes) | On attribute change |

---

## Acceptance Criteria

### Scenario 1: Happy Path - {Main Success Title}

**Type:** ✅ Happy Path  
**Journey Position:** Entry → Middle → Exit  
**Covers:** Main Flow steps 1 → N

**Given**
- {Persona} is logged in with {required_permission} permission
- {Required data exists} (e.g., Departments are configured)
- User navigated from {entry_point}

**When**
- {Persona} performs {action 1}
- {Persona} fills {required fields} with valid data
- {Persona} clicks "{submit_button}"

**Then**
- System validates all inputs successfully
- System creates/updates {entity} record
- System shows success message: "{message}"
- User is redirected to {destination}

**And** (Side Effects)
- System logs audit trail
- System sends notification to {recipient}
- System updates {related_entity} count

---

### Scenario 2: Alternative Path - {Alternative Route Title}

**Type:** 🔀 Alternative Path  
**Journey Position:** Middle  

**Given**
- {Different precondition that leads to alternative route}

**When**
- {Different user action}

**Then**
- {Different but still successful outcome}

---

### Scenario 3: Validation Error - {Field} Invalid

**Type:** ❌ Validation Error  
**Journey Position:** Middle → Loop back  
**Covers:** Alternative Flow Xa

**Given**
- {Persona} is on {form/screen}
- {Field} has invalid value: {example_invalid_value}

**When**
- {Persona} attempts to submit

**Then**
- System shows inline error on {field}: "{error_message}"
- Form remains open (no data loss)
- Other valid fields retain their values
- Focus moves to first error field

**Recovery**
- User corrects the {field}
- User can re-submit

---

### Scenario 4: Business Rule Error - {Rule} Violated

**Type:** ⚠️ Business Rule Error  
**Covers:** BR-{XXX}

**Given**
- {Condition that triggers business rule}

**When**
- {Persona} attempts action that violates rule

**Then**
- System shows error: "{business_rule_error_message}"
- Action is prevented
- Data remains unchanged

**Recovery**
- {How user can resolve this}

---

### Scenario 5: Permission Denied

**Type:** 🔒 Permission Denied  
**Journey Position:** Entry blocked

**Given**
- User is logged in but lacks {required_permission}
- OR User is not logged in

**When**
- User attempts to access this feature

**Then**
- System shows "Access Denied" message
- System suggests: "Contact your administrator" OR
- System redirects to login (if not authenticated)

---

### Scenario 6: Edit/Update Loop

**Type:** 🔄 Loop/Retry  
**Journey Position:** Middle → Loop back

**Given**
- {Entity} already exists
- {Persona} is viewing {entity} details

**When**
- {Persona} clicks "Edit"
- {Persona} modifies {fields}
- {Persona} clicks "Save"

**Then**
- System updates {entity}
- System shows "Changes saved" message
- User can edit again or navigate away

---

### Scenario 7: Cancel/Back Navigation

**Type:** 🔄 Loop/Retry  
**Journey Position:** Middle → Exit (previous)

**Given**
- {Persona} has unsaved changes on form

**When**
- {Persona} clicks "Cancel" or browser back

**Then**
- System shows confirmation: "Discard changes?"
- If Yes: Navigate to previous screen, discard changes
- If No: Stay on current screen

---

### Scenario 8: Empty State - No Data

**Type:** 📭 Empty State  
**Journey Position:** Entry

**Given**
- {Entity list} is empty (first-time user or no results)

**When**
- {Persona} navigates to {list screen}

**Then**
- System shows empty state illustration
- System shows message: "{friendly_empty_message}"
- System shows CTA button: "Add First {Entity}"
- CTA navigates to create flow

---

### Scenario 9: Session Timeout

**Type:** ⏰ Timeout  
**Journey Position:** Any → Exit

**Given**
- {Persona} has been inactive for 30+ minutes
- {Persona} has unsaved work

**When**
- Session expires

**Then**
- System shows "Session expired" modal
- System preserves form data in local storage (if possible)
- User can re-login and resume

---

### Scenario 10: Concurrent Modification

**Type:** ⚡ Concurrent  
**Journey Position:** Middle

**Given**
- {Persona A} is editing {entity}
- {Persona B} also edits same {entity}
- {Persona B} saves first

**When**
- {Persona A} attempts to save

**Then**
- System detects version conflict
- System shows: "This record was modified by {Persona B}"
- System offers: "Reload latest" or "Force overwrite"

---

## Scenario Coverage Checklist

Verify ALL applicable scenario types are covered:

| # | Type | Scenario # | Covered |
|---|------|------------|---------|
| 1 | Happy Path | Scenario 1 | ✓ |
| 2 | Alternative Path | Scenario 2 | ✓ / N/A |
| 3 | Validation Error | Scenario 3 | ✓ |
| 4 | Business Rule Error | Scenario 4 | ✓ / N/A |
| 5 | Permission Denied | Scenario 5 | ✓ |
| 6 | Loop/Retry (Edit) | Scenario 6 | ✓ |
| 7 | Loop/Retry (Cancel/Back) | Scenario 7 | ✓ |
| 8 | Empty State | Scenario 8 | ✓ / N/A |
| 9 | Session Timeout | Scenario 9 | ✓ |
| 10 | Concurrent Modification | Scenario 10 | ✓ / N/A |

---
