# View Recruitment Analytics Dashboard

**Story ID:** US-4.14  
**Epic:** Epic 0.7 - Scouting Network (ATS-Lite)  
**Persona:** HR Manager, Recruiter  
**Priority:** Nice to Have  
**Complexity:** M (2-3 days)

---

## User Story

> **As an** HR Manager,  
> **I want to** view comprehensive recruitment analytics and KPIs in a dashboard,  
> **So that** I can make data-driven decisions to improve hiring processes and outcomes.

---

## User Journey Context

### Entry Points
| Entry Source | Condition | User State |
|--------------|-----------|------------|
| Main navigation | Click "Analytics" | Reviewing performance |
| Dashboard widget | Click "View Full Analytics" | Quick insight to deep-dive |
| Scheduled report | Weekly email with link | Regular review |

### Exit Points
| Exit Condition | Destination | User State |
|----------------|-------------|------------|
| Insight identified | Action plan (e.g., adjust strategy) | Informed decision |
| Export report | Share with stakeholders | Communication |
| Drill-down | Detailed position/candidate view | Investigation |

---

## Business Logic

### Key Metrics Displayed

| Category | Metrics | Purpose |
|----------|---------|---------|
| **Pipeline Health** | Total active applications, Avg time in stage, Conversion rates per stage | Monitor flow efficiency |
| **Position Metrics** | Open positions, Avg time to fill, Fill rate | Track hiring speed |
| **Candidate Quality** | Avg fit score, Offer acceptance rate, Quality of hire | Assess effectiveness |
| **Source Performance** | Candidates by source, Conversion by source, Cost per hire | Optimize sourcing |
| **Interview Metrics** | Interviews scheduled, Avg feedback rating, Pass rate | Interview effectiveness |

---

## Acceptance Criteria (20 Scenarios)

### Scenario 1: Happy Path - View Main Dashboard

**Type:** ✅ Happy Path

**Given**
- I am HR Manager
- System has 3 months of recruitment data
- 5 open positions, 50 active applications

**When**
- I navigate to Analytics Dashboard
- Default view: Last 30 days

**Then**
- Dashboard displays key metrics:

**Overview Cards:**
```
┌────────────────┐ ┌────────────────┐ ┌────────────────┐
│ Active         │ │ Time to Fill   │ │ Offer          │
│ Applications   │ │                │ │ Acceptance     │
│      50        │ │   28 days      │ │     85%        │
│   +12 (↑31%)  │ │  -3 days (↓)   │ │   +5% (↑)     │
└────────────────┘ └────────────────┘ └────────────────┘
```

**Pipeline Funnel:**
```
New (20)          ████████████████████ 100%
↓
Screening (12)    ████████████ 60%
↓
Interview (7)     ███████ 35%
↓
Offer (3)         ███ 15%
↓
Hired (2)         ██ 10%
```

**Charts:**
- Applications over time (line chart)
- Hiring by department (pie chart)
- Source effectiveness (bar chart)
- Time to hire trend (area chart)

**Insights:**
- "💡 Screening stage taking 2× longer than average"
- "⚠️ Offer acceptance dropped 10% this month - investigate"
- "✅ LinkedIn source improved 5% conversion"

---

### Scenario 2: Happy Path - Filter by Date Range

**Type:** ✅ Happy Path

**Given**
- Dashboard loaded with 30-day view

**When**
- I change date range to "Last Quarter"

**Then**
- All metrics recalculate for 90 days
- Charts update with quarterly data
- Trends show longer-term patterns
- Comparison: "vs. Previous Quarter"

---

### Scenario 3: Happy Path - Drill Down to Position Details

**Type:** ✅ Happy Path

**Given**
- Dashboard shows "5 Open Positions"

**When**
- I click on "5 Open Positions" card

**Then**
- Navigate to position breakdown:
```
Position Details:
- Senior Backend Developer: 15 applications, 30 days open
- Frontend Developer: 10 applications, 20 days open
- Product Manager: 8 applications, 45 days open (⚠️ Long)
- UX Designer: 12 applications, 25 days open
- DevOps Engineer: 5 applications, 10 days open
```
- Can drill into each position's pipeline

---

### Scenario 4: Alternative Path - Compare Periods

**Type:** 🔀 Alternative Path

**Given**
- Want to see month-over-month improvement

**When**
- I select "Compare Periods"
- Choose: March 2026 vs. February 2026

**Then**
- Side-by-side comparison:
```
Metric              | March  | Feb    | Change
--------------------|--------|--------|--------
Applications        | 50     | 38     | +31% ↑
Time to Fill        | 28d    | 31d    | -3d ↓
Offer Acceptance    | 85%    | 80%    | +5% ↑
Cost per Hire       | ฿20k   | ฿25k   | -฿5k ↓
```
- Visual indicators: Green ↑ for improvements, Red ↓ for declines

---

### Scenario 5: Alternative Path - Export Dashboard Report

**Type:** 🔀 Alternative Path

**Given**
- Need to present to executive team

**When**
- I click "Export Report"
- Select format: PDF
- Include: All charts, metrics, insights

**Then**
- PDF generated with:
  - Cover page with date range
  - Executive summary
  - All visualizations
  - Key metrics table
  - Insights and recommendations
- Downloaded within 5 seconds
- Professional formatting

---

### Scenario 6: Alternative Path - Custom Widget Layout

**Type:** 🔀 Alternative Path

**Given**
- Want personalized dashboard view

**When**
- I click "Customize Dashboard"
- Drag widgets to reorder
- Hide "Cost per Hire" (not relevant to my role)
- Add "Interviews per Week" widget

**Then**
- Layout saved to my user preferences
- Dashboard shows customized view on next load
- Can reset to default anytime

---

### Scenario 7: Validation Error - Invalid Date Range

**Type:** ❌ Validation Error

**Given**
- Selecting custom date range

**When**
- I select start date: 2026-03-15
- End date: 2026-03-01 (before start date)

**Then**
- Error: "End date must be after start date"
- Date picker highlights error
- Dashboard not updated

---

### Scenario 8: Validation Error - No Data for Period

**Type:** ❌ Validation Error

**Given**
- Select date range: Jan 2025 (before system launch)

**When**
- Dashboard attempts to load

**Then**
- Warning: "No data available for selected period"
- Empty state: "System started Feb 2026"
- Suggestion: "Select date from Feb 2026 onwards"

---

### Scenario 9: Business Rule Error - Incomplete Data

**Type:** ⚠️ Business Rule Error

**Given**
- Some positions missing "time_to_fill" data
- Historical applications have incomplete status tracking

**When**
- Calculating average time to fill

**Then**
- Warning: "Data incomplete for 2 positions"
- Shows: "Avg Time to Fill: 28 days (calculated from 8 of 10 positions)"
- Disclaimer: "Metrics may be approximate due to incomplete data"

---

### Scenario 10: Permission Denied - Recruiter Limited View

**Type:** 🔒 Permission Denied

**Given**
- I am Recruiter (not HR Manager)
- Cost and budget metrics are restricted

**When**
- I view analytics dashboard

**Then**
- Can see: Pipeline metrics, conversion rates, time to hire
- Cannot see: Cost per hire, budget utilization, salary data
- Message: "Cost metrics available to HR Managers only"

---

### Scenario 11: Loop/Retry - Refresh Data

**Type:** 🔄 Loop/Retry

**Given**
- Dashboard loaded 2 hours ago
- New hires completed since then

**When**
- I click "Refresh" button

**Then**
- All metrics recalculate with latest data
- Cache cleared
- Updated timestamp shown: "Last updated: 2 minutes ago"
- Real-time accurate view

---

### Scenario 12: Empty State - No Active Recruitment

**Type:** 📭 Empty State

**Given**
- All positions filled
- No active applications

**When**
- View analytics dashboard

**Then**
- Empty state: "No active recruitment"
- Shows historical data: "View past 6 months"
- Message: "All positions filled. Great work! 🎉"
- Can still access archived analytics

---

### Scenario 13: Session Timeout - Viewing Dashboard

**Type:** ⏰ Timeout

**Given**
- Dashboard open for 45 minutes

**When**
- Session expires

**Then**
- Read-only mode continues (public dashboard)
- Filters preserved in URL
- No data loss
- Can continue viewing

---

### Scenario 14: Concurrent Modification - Real-Time Updates

**Type:** ⚡ Concurrent

**Given**
- Viewing dashboard
- Recruiter hires candidate

**When**
- Hire event occurs

**Then**
- Dashboard auto-updates (if WebSocket enabled)
- "Hired" count: 2 → 3
- Notification: "Dashboard updated (new hire)"
- Smooth transition, no full reload

---

### Scenario 15: Integration Error - Analytics Service Down

**Type:** ⚠️ Integration Error

**Given**
- Analytics calculation service unavailable

**When**
- Loading dashboard

**Then**
- Basic metrics load from database (cached)
- Advanced insights unavailable: "Advanced analytics temporarily unavailable"
- Core dashboard still functional
- Retry automatically every 2 minutes

---

### Scenario 16: Alternative Path - Scheduled Email Reports

**Type:** 🔀 Alternative Path

**Given**
- Want weekly analytics summary

**When**
- I configure: "Email weekly report every Monday 9 AM"

**Then**
- Email scheduled
- Every Monday, receive email with:
  - Key metrics summary
  - Week-over-week comparison
  - Top 3 insights
  - Link to full dashboard
- Can unsubscribe anytime

---

### Scenario 17: Alternative Path - Goal Tracking

**Type:** 🔀 Alternative Path

**Given**
- Set hiring goals: "Fill 10 positions by Q1 end"

**When**
- View dashboard with goals enabled

**Then**
- Progress indicator:
```
Q1 Hiring Goal Progress:
████████░░░░ 7 of 10 positions filled (70%)
23 days remaining in quarter

On Track: Yes ✓
```
- Forecast: "At current rate, will fill 8 positions by quarter end"

---

### Scenario 18: Loop/Retry - Save Custom Report

**Type:** 🔄 Loop/Retry

**Given**
- Created custom view with specific filters and date range

**When**
- I click "Save View"
- Name: "Monthly Backend Hiring Report"

**Then**
- View saved to my account
- Accessible from "Saved Reports" dropdown
- Can load anytime with one click
- Share link with team

---

### Scenario 19: Data Integrity - Data Quality Indicators

**Type:** ⚠️ Data Integrity

**Given**
- Some metrics have low confidence due to small sample

**When**
- Viewing "Average Interview Rating"
- Only 3 interviews completed

**Then**
- Warning icon: "⚠️ Low confidence (n=3)"
- Tooltip: "Need at least 10 data points for reliable metric"
- Metric shown but flagged

---

### Scenario 20: Performance - Large Dataset

**Type:** ⚠️ Performance

**Given**
- 2 years of data
- 500+ positions, 5,000+ applications

**When**
- Load annual analytics

**Then**
- Dashboard loads in <3 seconds
- Aggregated data pre-calculated
- Charts render smoothly
- No lag or timeout
- Pagination for detailed drill-downs

---

## Scenario Coverage: ✅ Complete (20 scenarios, all 10 types)

---

## UI/UX Requirements

### Analytics Dashboard Layout

```
╔═══════════════════════════════════════════════════════════╗
║ Recruitment Analytics                  [Last 30 days ▼]  ║
╠═══════════════════════════════════════════════════════════╣
║                                                           ║
║ Overview                                                  ║
║ ┌────────────┐ ┌────────────┐ ┌────────────┐           ║
║ │ Active     │ │ Time to    │ │ Offer      │           ║
║ │ Apps: 50   │ │ Fill: 28d  │ │ Accept: 85%│           ║
║ │ +31% ↑    │ │ -3d ↓     │ │ +5% ↑     │           ║
║ └────────────┘ └────────────┘ └────────────┘           ║
║                                                           ║
║ Pipeline Conversion Funnel                                ║
║ ┌─────────────────────────────────────────────────────┐  ║
║ │ New (20)      ████████████████████ 100%             │  ║
║ │ Screening(12) ████████████ 60%                      │  ║
║ │ Interview (7) ███████ 35%                           │  ║
║ │ Offer (3)     ███ 15%                               │  ║
║ │ Hired (2)     ██ 10%                                │  ║
║ └─────────────────────────────────────────────────────┘  ║
║                                                           ║
║ Applications Over Time                                    ║
║ ┌─────────────────────────────────────────────────────┐  ║
║ │   20│                          ╱╲                   │  ║
║ │   15│                    ╱─────╯  ╲                 │  ║
║ │   10│          ╱────────╯          ╲────            │  ║
║ │    5│   ╱─────╯                         ╲           │  ║
║ │    0│───────────────────────────────────────────    │  ║
║ │     Week1  Week2  Week3  Week4                      │  ║
║ └─────────────────────────────────────────────────────┘  ║
║                                                           ║
║ 💡 Key Insights:                                          ║
║ • Screening stage 2× slower than target                  ║
║ • LinkedIn conversion improved 5%                        ║
║ • 3 positions open >45 days - needs attention           ║
║                                                           ║
║ [Export PDF] [Schedule Report] [Customize] [Refresh]     ║
╚═══════════════════════════════════════════════════════════╝
```

**END OF US-4.14**
