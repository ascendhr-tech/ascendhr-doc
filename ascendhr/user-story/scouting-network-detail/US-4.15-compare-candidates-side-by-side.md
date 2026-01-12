# Compare Candidates Side-by-Side

**Story ID:** US-4.15  
**Epic:** Epic 0.7 - Scouting Network (ATS-Lite)  
**Persona:** Recruiter, Hiring Manager  
**Priority:** Nice to Have  
**Complexity:** S (1-2 days)

---

## User Story

> **As a** Hiring Manager,  
> **I want to** compare multiple candidates side-by-side in a single view,  
> **So that** I can make informed decisions when choosing between finalists.

---

## User Journey Context

### Entry Points
| Entry Source | Condition | User State |
|--------------|-----------|------------|
| Kanban board | Select 2-4 candidates, click "Compare" | Evaluating options |
| Application list | Multi-select candidates | Making final decision |
| Offer stage | Choosing between top candidates | Critical decision point |

### Exit Points
| Exit Condition | Destination | User State |
|----------------|-------------|------------|
| Decision made | Move preferred candidate to Offer | Clear choice |
| Need more info | Individual candidate details | Further evaluation |
| Export comparison | Share with stakeholders | Collaborative decision |

---

## Business Logic

### Comparison Dimensions

| Category | Fields Compared | Visual |
|----------|----------------|--------|
| **Profile** | Name, photo, experience, education | Side-by-side cards |
| **Fit Score** | Overall score, attribute breakdown | Color-coded badges |
| **Interview** | Feedback ratings, recommendations | Star ratings |
| **Logistics** | Availability, salary expectations, location | Table format |
| **Timeline** | Days in pipeline, responsiveness | Bar chart |

---

## Acceptance Criteria (20 Scenarios)

### Scenario 1: Happy Path - Compare 2 Candidates

**Type:** ✅ Happy Path

**Given**
- Position "Senior Backend Developer" has 3 finalists
- I want to compare top 2: Alex Chen and Jane Doe

**When**
- I select Alex and Jane from Kanban
- I click "Compare Candidates"

**Then**
- Comparison view opens showing:

```
╔═══════════════════════════════════════════════════════╗
║ Candidate Comparison                                  ║
╠═══════════════════════════════════════════════════════╣
║           Alex Chen            |    Jane Doe          ║
║                                |                      ║
║ Fit Score: 95% 🟢             | Fit Score: 92% 🟢   ║
║                                |                      ║
║ Technical Skills:              | Technical Skills:    ║
║ Backend:      18/16 ✓         | Backend:      17/16 ✓║
║ Database:     17/15 ✓         | Database:     16/15 ✓║
║ Architecture: 15/14 ✓         | Architecture: 14/14 ✓║
║                                |                      ║
║ Interview Feedback:            | Interview Feedback:  ║
║ Overall: ⭐⭐⭐⭐⭐ (5/5)       | Overall: ⭐⭐⭐⭐☆ (4/5)║
║ Recommendation: Strong Hire    | Recommendation: Hire ║
║                                |                      ║
║ Experience:                    | Experience:          ║
║ 7 years                        | 5 years              ║
║                                |                      ║
║ Salary Expectation:            | Salary Expectation:  ║
║ ฿90,000/month                 | ฿80,000/month        ║
║                                |                      ║
║ Availability:                  | Availability:        ║
║ 1 month notice                 | Immediate            ║
║                                |                      ║
║ Source: LinkedIn               | Source: Referral     ║
║ Applied: 25 days ago           | Applied: 20 days ago ║
╚═══════════════════════════════════════════════════════╝

Recommendation: Alex Chen has higher ratings but Jane has 
better availability. Consider if timeline is critical.

[Export PDF] [Select Winner] [View Details]
```

- Clear visual differentiation
- Winner/better values highlighted in bold/green
- Actionable recommendation provided

---

### Scenario 2: Happy Path - Compare 4 Candidates (Panel View)

**Type:** ✅ Happy Path

**Given**
- 4 finalists for executive role
- Need comprehensive comparison

**When**
- Select all 4 candidates
- Open comparison

**Then**
- Horizontal scroll table view:
```
Metric      | Alex    | Jane    | Mike    | Sarah
------------|---------|---------|---------|--------
Fit Score   | 95% 🟢 | 92% 🟢 | 88% 🟡 | 85% 🟡
Interview   | 5/5     | 4/5     | 4/5     | 5/5
Experience  | 7y      | 5y      | 10y     | 6y
Salary      | ฿90k    | ฿80k    | ฿110k   | ฿85k
Available   | 1mo     | Now     | 2mo     | 1mo
```
- Sortable columns
- Best value per row highlighted
- Can expand/collapse categories

---

### Scenario 3: Alternative Path - Focus on Specific Attributes

**Type:** 🔀 Alternative Path

**Given**
- Technical skills most important for this role

**When**
- I toggle "Show Only: Technical Skills"

**Then**
- Simplified comparison focusing on:
  - Backend Development scores
  - Database Design scores
  - System Architecture scores
  - Coding interview performance
- Other attributes collapsed/hidden
- Focused decision-making

---

### Scenario 4: Alternative Path - Add/Remove Candidates

**Type:** 🔀 Alternative Path

**Given**
- Currently comparing Alex and Jane
- Want to add Mike to comparison

**When**
- I click "+ Add Candidate"
- Select Mike from dropdown

**Then**
- Mike added to comparison view
- Now showing 3 columns
- Layout adjusts automatically
- Can remove any candidate by clicking "×"

---

### Scenario 5: Alternative Path - Export Comparison Report

**Type:** 🔀 Alternative Path

**Given**
- Comparison complete
- Need to share with CEO for approval

**When**
- I click "Export Comparison"
- Select format: PDF

**Then**
- PDF generated with:
  - Header: Position title, date
  - Side-by-side comparison table
  - Charts (fit score, experience comparison)
  - Interview feedback summary
  - Recommendation section
- Professional formatting for stakeholders

---

### Scenario 6: Validation Error - Too Many Candidates

**Type:** ❌ Validation Error

**Given**
- Attempting to compare 6 candidates

**When**
- Select 6th candidate

**Then**
- Error: "Maximum 5 candidates can be compared at once"
- Suggestion: "Compare in smaller groups for clarity"
- 6th candidate not added

---

### Scenario 7: Validation Error - Same Candidate Selected Twice

**Type:** ❌ Validation Error

**Given**
- Alex already in comparison

**When**
- Attempt to add Alex again

**Then**
- Error: "Alex Chen is already in comparison"
- Duplicate prevented
- Show existing candidates clearly

---

### Scenario 8: Validation Error - Candidates from Different Positions

**Type:** ❌ Validation Error

**Given**
- Select candidates from different positions

**When**
- Attempt to compare

**Then**
- Warning: "Candidates are from different positions"
- Message: "Comparison works best for same position"
- Option to proceed anyway (for cross-position comparison)
- Or cancel and reselect

---

### Scenario 9: Business Rule Error - Insufficient Data

**Type:** ⚠️ Business Rule Error

**Given**
- Comparing Alex (complete profile) with Bob (minimal data)
- Bob has no interview feedback, incomplete attributes

**When**
- View comparison

**Then**
- Bob's column shows:
  - Interview: "Not conducted yet"
  - Attributes: "Incomplete - 3 of 8 rated"
- Warning: "Incomplete data for Bob - comparison limited"
- Suggestion: "Complete interviews before final comparison"

---

### Scenario 10: Permission Denied - Interviewer Limited View

**Type:** 🔒 Permission Denied

**Given**
- I am Interviewer (not Hiring Manager)
- Salary data is restricted

**When**
- View comparison

**Then**
- Can see: Fit scores, interview feedback, technical skills
- Cannot see: Salary expectations, cost data
- Message: "Salary data visible to Hiring Managers only"

---

### Scenario 11: Loop/Retry - Save Comparison

**Type:** 🔄 Loop/Retry

**Given**
- Created detailed comparison
- Want to review later

**When**
- Click "Save Comparison"
- Name: "Backend Developer Finalists - March 2026"

**Then**
- Comparison saved to my account
- Accessible from "Saved Comparisons"
- Can reload with same candidates and filters
- Share link with team

---

### Scenario 12: Empty State - No Candidates Selected

**Type:** 📭 Empty State

**Given**
- Clicked "Compare" without selections

**When**
- Comparison page opens

**Then**
- Empty state: "Select candidates to compare"
- Instructions: "Go to Kanban and select 2-5 candidates"
- Quick link: "Back to Kanban"

---

### Scenario 13: Session Timeout - Mid-Comparison

**Type:** ⏰ Timeout

**Given**
- Comparison view open for 40 minutes

**When**
- Session expires

**Then**
- Read-only view continues
- Selected candidates preserved in URL
- After re-login: Comparison reloads

---

### Scenario 14: Concurrent Modification - Candidate Updated During Comparison

**Type:** ⚡ Concurrent

**Given**
- Viewing comparison of Alex and Jane
- Recruiter updates Alex's fit score

**When**
- Fit score changes: 95% → 97%

**Then**
- Real-time update (if WebSocket)
- Alex's fit score updates in comparison view
- Notification: "Alex Chen's profile updated"
- Option to refresh comparison

---

### Scenario 15: Integration Error - Missing Interview Data

**Type:** ⚠️ Integration Error

**Given**
- Interview feedback service temporarily down

**When**
- Loading comparison

**Then**
- Other data loads successfully
- Interview section shows: "Temporarily unavailable"
- Comparison still functional
- Non-blocking error

---

### Scenario 16: Alternative Path - Weighted Comparison

**Type:** 🔀 Alternative Path

**Given**
- Technical skills 60% important, soft skills 40%

**When**
- I enable "Weighted Scoring"
- Set weights: Technical 60%, Soft Skills 40%

**Then**
- Calculated weighted scores:
  ```
  Alex: (95×0.6) + (90×0.4) = 93
  Jane: (92×0.6) + (95×0.4) = 93.2
  
  Winner: Jane (by weighted score)
  ```
- Shows impact of different weightings

---

### Scenario 17: Alternative Path - Timeline Comparison

**Type:** 🔀 Alternative Path

**Given**
- Want to see who progressed faster

**When**
- View "Timeline" tab in comparison

**Then**
- Shows:
```
Alex: Applied → Hired (28 days)
  New: 2 days
  Screening: 5 days
  Interview: 15 days
  Offer: 6 days

Jane: Applied → Current (20 days, in Interview)
  New: 1 day
  Screening: 4 days
  Interview: 15 days (ongoing)
```
- Visual timeline chart
- Identifies bottlenecks

---

### Scenario 18: Loop/Retry - Compare Different Groups

**Type:** 🔄 Loop/Retry

**Given**
- Compared Alex vs. Jane (group A)
- Now want to compare Mike vs. Sarah (group B)

**When**
- Click "New Comparison"
- Select Mike and Sarah

**Then**
- Previous comparison closed
- New comparison loads
- Can switch between saved comparisons
- History maintained

---

### Scenario 19: Data Integrity - Normalize Scores

**Type:** ⚠️ Data Integrity

**Given**
- Different interviewers use different rating scales
- Alex rated by lenient interviewer (avg 4.5/5)
- Jane rated by strict interviewer (avg 3.2/5)

**When**
- Viewing comparison

**Then**
- Option: "Normalize Interview Scores"
- Adjusts for interviewer bias
- Shows both raw and normalized scores
- Fair comparison

---

### Scenario 20: Performance - Load Large Comparison

**Type:** ⚠️ Performance

**Given**
- Comparing 5 candidates
- Each with extensive data (10 interviews, 20 attributes)

**When**
- Load comparison

**Then**
- Renders in <2 seconds
- Lazy load non-visible sections
- Smooth scrolling
- No lag

---

## Scenario Coverage: ✅ Complete (20 scenarios, all 10 types)

---

## UI/UX Requirements

### Comparison View (2 Candidates)

```
╔═══════════════════════════════════════════════════════════╗
║ Compare Candidates                        [Export] [Save] ║
╠═══════════════════════════════════════════════════════════╣
║                                                           ║
║  ┌─────────────────────┐   ┌─────────────────────┐      ║
║  │ 👤 Alex Chen        │   │ 👤 Jane Doe         │      ║
║  │                     │   │                     │      ║
║  │ ┌─────────┐        │   │ ┌─────────┐        │      ║
║  │ │   95%   │ 🟢     │   │ │   92%   │ 🟢     │      ║
║  │ └─────────┘        │   │ └─────────┘        │      ║
║  │                     │   │                     │      ║
║  │ Backend:    18/16 ✓│   │ Backend:    17/16 ✓│      ║
║  │ Database:   17/15 ✓│   │ Database:   16/15 ✓│      ║
║  │ System:     15/14 ✓│   │ System:     14/14 ✓│      ║
║  │                     │   │                     │      ║
║  │ Interview: ⭐⭐⭐⭐⭐│   │ Interview: ⭐⭐⭐⭐☆│      ║
║  │ Strong Hire         │   │ Hire                │      ║
║  │                     │   │                     │      ║
║  │ Experience: 7y      │   │ Experience: 5y      │      ║
║  │ Salary: ฿90k        │   │ Salary: ฿80k        │      ║
║  │ Available: 1mo      │   │ Available: Now ✓   │      ║
║  │                     │   │                     │      ║
║  │ LinkedIn            │   │ Referral ✓          │      ║
║  │ 25 days ago         │   │ 20 days ago         │      ║
║  │                     │   │                     │      ║
║  │ [View Full Profile] │   │ [View Full Profile] │      ║
║  └─────────────────────┘   └─────────────────────┘      ║
║                                                           ║
║ 💡 Recommendation:                                        ║
║ Alex has stronger technical ratings (+3 points) and      ║
║ higher interview scores. Jane offers immediate           ║
║ availability and lower salary. Choose Alex if quality    ║
║ is priority, Jane if timeline is critical.               ║
║                                                           ║
║ [Move Alex to Offer] [Move Jane to Offer] [Compare More] ║
╚═══════════════════════════════════════════════════════════╝
```

### Comparison Table (4+ Candidates)

```
╔═══════════════════════════════════════════════════════════╗
║ Candidate Comparison - Senior Backend Developer          ║
╠═══════════════════════════════════════════════════════════╣
║                                                           ║
║ Metric          │ Alex  │ Jane  │ Mike  │ Sarah │ Best  ║
║ ────────────────┼───────┼───────┼───────┼───────┼────── ║
║ Fit Score       │ 95% 🟢│ 92% 🟢│ 88% 🟡│ 85% 🟡│ Alex  ║
║ Interview       │ 5/5   │ 4/5   │ 4/5   │ 5/5   │ Tie   ║
║ Backend Dev     │ 18/16 │ 17/16 │ 16/16 │ 15/16 │ Alex  ║
║ Experience      │ 7y    │ 5y    │ 10y ✓ │ 6y    │ Mike  ║
║ Salary Expected │ ฿90k  │ ฿80k ✓│ ฿110k │ ฿85k  │ Jane  ║
║ Availability    │ 1mo   │ Now ✓ │ 2mo   │ 1mo   │ Jane  ║
║ Source          │ LI    │ Ref ✓ │ LI    │ Job   │ Ref   ║
║ Days in Pipe    │ 25    │ 20 ✓  │ 30    │ 22    │ Jane  ║
║                                                           ║
║ Summary:                                                  ║
║ • Alex: Best technical fit (4/8 metrics)                 ║
║ • Jane: Best logistics (3/8 metrics + referral)          ║
║ • Mike: Most experience but highest salary               ║
║ • Sarah: Balanced but lower fit score                    ║
║                                                           ║
║ [Sort by ▼] [Filter Metrics] [Export] [Select Winner]    ║
╚═══════════════════════════════════════════════════════════╝
```

**END OF US-4.15**
