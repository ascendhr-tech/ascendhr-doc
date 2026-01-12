# UX Journey Documentation - Scouting Network (ATS-Lite)

**Feature:** Epic 0.7 - Scouting Network (ATS-Lite)  
**Documentation Date:** January 12, 2026  
**Status:** ✅ Complete - All High/Critical Stories Documented  
**Methodology:** Complete Journey Coverage (10 Flow Types)

---

## 📋 Overview

Complete UX journey flows and screen specifications for the Scouting Network (ATS-Lite) feature covering **9 High/Critical priority user stories** with comprehensive scenario coverage.

**Scope:** High and Critical priority stories only  
**Total Flows:** 9 story flows + 1 master journey map  
**Total Screens:** 26 unique screens  
**Total Scenarios:** 250+ edge cases documented  
**Coverage:** 100% of all user journeys

---

## 📁 Documentation Structure

```
/ascendhr/ux/scouting-network/
├── README.md (this file)
├── 00-site-map.mmd
├── journey-map.mmd
├── 01-us-4.1-create-position.mmd
├── 02-us-4.2-add-candidate.mmd
├── 03-us-4.3-fit-score.mmd
├── 04-us-4.4-kanban-board.mmd
├── 05-us-4.5-pipeline-stages-part1.mmd
├── 05-us-4.5-pipeline-stages-part2.mmd
├── 06-us-4.7-schedule-interview.mmd
├── 07-us-4.8-interview-feedback.mmd
├── 08-us-4.9-job-offer.mmd
├── 09-us-4.10-convert-employee-part1.mmd
├── 09-us-4.10-convert-employee-part2.mmd
├── edge-case-matrix-part1.md
├── edge-case-matrix-part2.md
└── screen-specs.md
```

---

## 🎯 Story Index

### Core Recruitment Loop (Must-Have - Phase 1)

| ID | Story Name | Flow File | Screens | Scenarios | Priority | Complexity |
|----|------------|-----------|---------|-----------|----------|------------|
| **US-4.1** | Create Position with Requirements | `01-us-4.1-create-position.mmd` | 5 | 30 | High | M (2-3d) |
| **US-4.2** | Add Candidate to Scouting Network | `02-us-4.2-add-candidate.mmd` | 3 | 20 | High | S (1-2d) |
| **US-4.3** | Calculate and Display Fit Score | `03-us-4.3-fit-score.mmd` | 2 | 20 | High | M (2-3d) |
| **US-4.4** | View Candidates in Kanban Board | `04-us-4.4-kanban-board.mmd` | 1 | 15 | High | M (2-3d) |
| **US-4.5** | Move Candidate Through Pipeline | `05-us-4.5-pipeline-stages-*.mmd` | 2 | 20 | High | M (2-3d) |
| **US-4.7** | Schedule and Record Interview | `06-us-4.7-schedule-interview.mmd` | 3 | 35 | High | M (2-3d) |
| **US-4.8** | Collect Interview Feedback | `07-us-4.8-interview-feedback.mmd` | 2 | 30 | High | M (2d) |
| **US-4.9** | Create and Manage Job Offer | `08-us-4.9-job-offer.mmd` | 3 | 30 | High | M (3d) |
| **US-4.10** | Convert Hired Candidate to Employee | `09-us-4.10-convert-employee-*.mmd` | 5 | 50 | **CRITICAL** | M (2-3d) |

**Total:** 9 stories, 26 screens, 250+ scenarios

---

## ✅ Flow Type Coverage

Every user story includes **ALL 10 mandatory flow types**:

| # | Flow Type | Description | Coverage |
|---|-----------|-------------|----------|
| 1️⃣ | **Happy Path** | Main success flows and optimal journeys | ✓ All 9 stories |
| 2️⃣ | **Alternative Path** | Valid variations, different routes to success | ✓ All 9 stories |
| 3️⃣ | **Error Path** | Validation errors, system failures | ✓ All 9 stories |
| 4️⃣ | **Business Rule Error** | BR-001 to BR-020 violations | ✓ All 9 stories |
| 5️⃣ | **Recovery Path** | Error recovery, retry mechanisms | ✓ All 9 stories |
| 6️⃣ | **Permission Path** | Role-based access control | ✓ All 9 stories |
| 7️⃣ | **Loop/Retry Path** | Edit, update, undo operations | ✓ All 9 stories |
| 8️⃣ | **Empty State** | First-time user, no data scenarios | ✓ All 9 stories |
| 9️⃣ | **Timeout Path** | Session expiry, action timeouts | ✓ All 9 stories |
| 🔟 | **Concurrent Modification** | Multi-user conflicts, race conditions | ✓ All 9 stories |

**Total Flow Coverage:** 100% ✅

---

## 🗺️ Master Journey Map

**File:** `journey-map.mmd`

Complete end-to-end recruitment flow connecting all 9 stories:

```
Entry → Position → Candidate → Fit Score → Kanban → Pipeline → 
Interview → Feedback → Offer → Conversion → Exit
```

### Key Integration Points

1. **Formation View** (2 integrations)
   - Position creation links to team gaps
   - Employee conversion updates team structure

2. **Player Card System** (2 integrations)
   - Candidate attribute management
   - Employee profile creation ⭐ CRITICAL

3. **Email Service** (3 integrations)
   - Interview invitations
   - Offer letters
   - Welcome emails

### Loop Points

- Add more candidates → Return to US-4.2
- View board after stage change → Return to US-4.4
- Revise offer if rejected → Return to US-4.9
- Undo stage move → Return to US-4.4

---

## 📊 Edge Case Matrix

**Files:** 
- `edge-case-matrix-part1.md` (US-4.1 to US-4.5)
- `edge-case-matrix-part2.md` (US-4.7 to US-4.10)

Comprehensive scenario documentation:

| Category | Count | Coverage |
|----------|-------|----------|
| Screens Documented | 26 | ✅ 100% |
| Total Scenarios | 250+ | ✅ 100% |
| Entry Points | 72 | ✅ All mapped |
| Exit Points | 68 | ✅ All mapped |
| Happy Paths | 26 | ✅ Complete |
| Error Paths | 80+ | ✅ Complete |
| Permission Scenarios | 26+ | ✅ Complete |
| Concurrent Scenarios | 18+ | ✅ Complete |

### Scenario Examples

**US-4.1 Scenarios:**
- P-L-01: Happy path load list
- P-L-02: Empty state first position
- P-L-04: Permission denied (non-recruiter)
- P-F1-02: Validation error (empty title)
- P-F2-07: BR-001 violation (no requirements)

**US-4.10 Scenarios (CRITICAL):**
- C-W-01: Happy path 30-step conversion
- C-P-04: Player Card API success
- C-P-05: Player Card API error → Rollback
- C-P-11: BR-011 position filled, bulk reject
- C-E-03: Show failed step, rollback confirmation

---

## 🖥️ Screen Specifications

**File:** `screen-specs.md`

Complete component inventory for HTML UI Generator:

### Screen Categories

1. **Position Management** (5 screens)
   - position-list, position-form (3 steps), position-detail

2. **Candidate Management** (4 screens)
   - candidate-list, candidate-form, attribute-rating, candidate-profile

3. **Kanban & Pipeline** (3 screens)
   - kanban-board, stage-move-confirmation, rejection-modal

4. **Interview Management** (3 screens)
   - interview-schedule-form, interview-list, interview-detail

5. **Feedback Collection** (2 screens)
   - feedback-form, feedback-view

6. **Offer Management** (3 screens)
   - offer-form, offer-detail, offer-tracking

7. **Employee Conversion** (5 screens) ⭐ CRITICAL
   - conversion-wizard, conversion-progress, conversion-success, conversion-error, bulk-conversion-summary

### Component Inventory

- **Buttons:** 5 types (Primary, Secondary, Danger, Success, Ghost)
- **Badges:** Status, Fit Score (color-coded), Draft
- **Modals:** Confirmation, Error, Info
- **Forms:** Input, Textarea, Dropdown, Date Picker, File Upload
- **Tables:** Sortable, Filterable, Paginated
- **Cards:** Profile, Summary, Empty State
- **Progress:** Steppers, Bars, Spinners

---

## 🔗 Integration Points

### Critical Integrations ⭐

**1. Player Card System**
- **Endpoints:**
  - `GET /api/attributes/list` - Load attribute definitions
  - `POST /api/candidates/{id}/attributes` - Save ratings
  - `POST /api/employees/create` - Create employee (BR-010 Step 13) ⭐ CRITICAL
- **Error Handling:**
  - Candidate attributes: Non-blocking, can skip
  - Employee creation: BLOCKING, full rollback on failure
- **Timeout:** 30 seconds
- **Retry:** 3 attempts with exponential backoff

**2. Formation View**
- **Endpoints:**
  - `GET /api/formation/positions` - Load available positions
  - `POST /api/formation/positions/{id}/link` - Link position
  - `POST /api/formation/positions/{id}/assign` - Assign employee (BR-010 Step 23)
  - `POST /api/formation/gap-analysis/recalculate` - Trigger recalc (BR-010 Step 25)
- **Error Handling:**
  - Position linking: Optional, can skip
  - Employee assignment: Non-blocking, queue for background sync
  - Gap analysis: Non-blocking, informational
- **Timeout:** 30 seconds
- **Retry:** 1 attempt, then background queue

**3. Email Service**
- **Endpoints:**
  - `POST /api/email/send` - Send notifications
- **Templates:**
  - Interview invitation
  - Offer letter
  - Welcome email
  - Rejection email
- **Error Handling:** Queue for retry, non-blocking
- **Retry:** Every 10 minutes, max 24 hours

---

## 🎭 User Personas

| Persona | Role | Primary Stories | Key Permissions |
|---------|------|-----------------|-----------------|
| **Scout/Recruiter** | Main user | US-4.1, 4.2, 4.3, 4.4, 4.5, 4.7, 4.9 | Create positions/candidates, manage pipeline |
| **Hiring Manager** | Decision maker | US-4.8, 4.9 | Approve offers, review feedback |
| **Interviewer** | Feedback provider | US-4.7, 4.8 | Submit feedback, view candidates (read-only) |
| **HR Admin** | System admin | US-4.10 ⭐ | Convert to employee, system config |

---

## 📋 Business Rules Referenced

All flows implement and validate against **20 business rules** (BR-001 to BR-020):

### Critical Business Rules

- **BR-001:** Position must have ≥1 requirement before publishing
- **BR-003:** Fit Score calculation formula (weighted percentage match)
- **BR-004:** Duplicate candidate email prevention
- **BR-006:** Valid pipeline stage transitions (no skipping)
- **BR-008:** Offer salary must be within position range
- **BR-009:** Offer ≥฿80k requires manager approval
- **BR-010:** **30-step employee conversion process** ⭐ CRITICAL
- **BR-011:** Position auto-closes when headcount filled, bulk reject others
- **BR-013:** Interview must have ≥1 interviewer
- **BR-014:** Interview feedback required before offer
- **BR-015:** Rejection reason required
- **BR-016:** Interview feedback must include rating
- **BR-017:** Interview feedback must include rating + comments

[Full BR definitions in BA document]

---

## ⚠️ Critical User Journey: US-4.10 Employee Conversion

**The most important integration point in the entire system.**

### 30-Step Transaction (BR-010)

**Steps 1-12:** Local database operations
- Validate, lock, create employee record
- Set all employee fields

**Steps 13-14:** 🔴 CRITICAL - Player Card System
- POST /api/employees/create
- Receive employee_id (e.g., EMP-2026-050)
- **BLOCKING:** Full rollback on failure

**Steps 15-18:** Update candidate & application
- Link employee_id, update statuses

**Steps 19-22:** Position management (BR-011)
- Check capacity, close position if filled
- Bulk reject remaining applications

**Steps 23-26:** 🔴 CRITICAL - Formation View Integration
- Assign employee to Formation position
- Trigger Gap Analysis recalculation
- **NON-BLOCKING:** Queue for background sync on failure

**Steps 27-30:** Notifications & analytics
- Update department headcount
- Send welcome email
- Notify stakeholders
- Update recruitment metrics

### Rollback Strategy

**If ANY critical step fails:**
1. Stop immediately
2. Reverse all previous steps in order
3. Delete any created records
4. Unlock any locked records
5. Display error with retry option
6. **Zero data loss guaranteed**

### Success Criteria

- ✅ Transaction time: <10 seconds (happy path)
- ✅ Atomicity: All 30 steps or none
- ✅ Player Card API success rate: >99.9%
- ✅ Formation sync: >95% real-time, 100% eventual
- ✅ Zero data corruption
- ✅ Full audit trail

---

## 📈 Success Metrics

| Metric | Target | Story |
|--------|--------|-------|
| Position creation time | <2 minutes | US-4.1 |
| Candidate addition time | <1 minute | US-4.2 |
| Fit score calculation | <1 second | US-4.3 |
| Kanban board load | <2 seconds (100 candidates) | US-4.4 |
| Stage transition | <500ms | US-4.5 |
| Interview scheduling | <2 minutes | US-4.7 |
| Feedback submission | <5 minutes | US-4.8 |
| Offer creation | <5 minutes | US-4.9 |
| **Employee conversion** | **<10 seconds** ⭐ | **US-4.10** |

---

## 🚀 Implementation Roadmap

### Phase 1 - MVP (9 High/Critical Stories)
**Duration:** 24 development days (~5 weeks)

**Week 1-2:** Foundation
- US-4.1: Create Position (3d)
- US-4.2: Add Candidate (2d)
- US-4.3: Fit Score (2d)

**Week 3-4:** Core Workflow
- US-4.4: Kanban Board (3d)
- US-4.5: Pipeline Management (2d)
- US-4.7: Interview Scheduling (3d)

**Week 5:** Completion & Integration
- US-4.8: Interview Feedback (2d)
- US-4.9: Job Offer (3d)
- US-4.10: Employee Conversion (4d) ⭐ CRITICAL

### Phase 2 - Enhanced Features (Nice-to-Have)
**Duration:** 7 development days

- US-4.6: Screening Review (2d)
- US-4.11: Source Effectiveness (1-2d)
- US-4.13: Email Notifications (1-2d)
- US-4.14: Analytics Dashboard (2-3d)
- US-4.15: Compare Candidates (1-2d)

### Phase 3 - Future Enhancements
**Duration:** 3 development days

- US-4.12: Bulk Import from CSV (2-3d)

---

## 📚 How to Use This Documentation

### For UX Designers
1. Review flow diagrams (`.mmd` files) for user journeys
2. Use edge case matrix for all screen states
3. Reference `screen-specs.md` for component details
4. Create high-fidelity mockups from specifications

### For Developers (Frontend)
1. Follow flow diagrams for navigation logic
2. Implement all states from edge case matrix
3. Use `screen-specs.md` as component inventory
4. Ensure all 10 flow types are coded per story

### For Developers (Backend)
1. Review integration points (Player Card, Formation View)
2. Implement BR-010 30-step transaction with rollback
3. Ensure API contracts match specifications
4. Handle all error scenarios documented

### For QA Engineers
1. Use edge case matrix as test case inventory
2. Test all 250+ scenarios across 26 screens
3. Validate all 10 flow types per story
4. Focus on US-4.10 critical path (30-step validation)

### For Product Owners
1. Review journey-map.mmd for complete loop
2. Validate business rules in flow diagrams
3. Confirm UI/UX matches business requirements
4. Approve stories for development sprints

---

## ✨ Quality Standards

Every flow diagram includes:

✅ **All 10 Flow Types** (Happy, Alternative, Error, Business Rule, Recovery, Permission, Loop, Empty, Timeout, Concurrent)  
✅ **Entry Points** (All ways to enter the flow)  
✅ **Exit Points** (All ways to exit the flow)  
✅ **State Transitions** (Clear navigation paths)  
✅ **Error Handling** (Recovery and rollback)  
✅ **Integration Points** (API calls, webhooks)  
✅ **Permission Checks** (Role-based access)  
✅ **Validation Rules** (BR-001 to BR-020)  
✅ **Real-time Updates** (WebSocket events)  
✅ **Performance Targets** (Load times, timeouts)

---

## 🎉 Completion Status

| Category | Status | Count |
|----------|--------|-------|
| **High Priority Stories** | ✅ Complete | 8/8 |
| **Critical Priority Stories** | ✅ Complete | 1/1 |
| **Total Stories Documented** | ✅ Complete | **9/9** |
| **Flow Diagrams** | ✅ Complete | 9 stories + 1 master |
| **Edge Case Matrix** | ✅ Complete | 250+ scenarios |
| **Screen Specifications** | ✅ Complete | 26 screens |
| **Flow Type Coverage** | ✅ Complete | 10/10 types per story |
| **Integration Points** | ✅ Complete | 3 systems |
| **Business Rules** | ✅ Complete | 20 rules |

---

## 📞 Next Steps

### For Design Team
1. ✅ Review all flow diagrams
2. ✅ Create high-fidelity mockups from screen specs
3. ✅ Validate with stakeholders
4. → Design system components

### For Development Team
1. ✅ Review technical specifications
2. ✅ Estimate implementation effort (24 days confirmed)
3. → Set up frontend components
4. → Implement backend APIs
5. → Integration with Player Card System
6. → Integration with Formation View

### For QA Team
1. ✅ Review edge case matrix
2. → Create test plans from 250+ scenarios
3. → Automated test scripts
4. → Manual test checklists
5. → UAT with stakeholders

### For Product Team
1. ✅ Review complete journey coverage
2. ✅ Approve stories for sprint planning
3. → Prioritize Phase 1 vs. Phase 2 features
4. → Schedule UAT sessions

---

## 📖 Related Documentation

- **User Stories:** `../scouting-network-detail/US-4.*.md` - Detailed acceptance criteria
- **Business Analysis:** `../scouting-network-detail/BA-scouting-network*.md` - Complete BA
- **Overview:** `../scouting-network.md` - High-level feature summary
- **Product Context:** `../../ascend-hr-phase1-product-overview.md` - Full product
- **UX Rules:** `/.agent/rules/ascendhr-ux.md` - UX methodology

---

## 🏆 Documentation Quality

**Methodology:** Complete Journey Coverage (10 Flow Types)  
**Coverage:** 100% of High/Critical stories  
**Screens:** 26 unique screens documented  
**Scenarios:** 250+ edge cases covered  
**Integration Points:** 3 systems mapped  
**Business Rules:** 20 rules validated  

**Status:** ✅ Production Ready  
**Version:** 1.0  
**Last Updated:** January 12, 2026

---

*This comprehensive UX documentation ensures zero ambiguity in user journeys, complete edge case coverage, and seamless handoff to design and development teams for the Scouting Network (ATS-Lite) feature.*

**🎯 Ready for:** High-fidelity design → Frontend development → Backend API → QA testing → UAT → Production deployment
