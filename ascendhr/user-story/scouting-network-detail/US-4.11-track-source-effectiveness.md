# Track and Display Source Effectiveness

**Story ID:** US-4.11  
**Epic:** Epic 0.7 - Scouting Network (ATS-Lite)  
**Persona:** Scout/Recruiter, HR Manager  
**Priority:** Nice to Have  
**Complexity:** S (1-2 days)

---

## User Story

> **As an** HR Manager,  
> **I want to** track which candidate sources (LinkedIn, Referrals, Job Boards) are most effective,  
> **So that** I can optimize recruitment spending and sourcing strategies.

---

## User Journey Context

### Entry Points
| Entry Source | Condition | User State |
|--------------|-----------|------------|
| Analytics dashboard | Click "Source Effectiveness" widget | Analyzing recruitment |
| Source detail page | Click specific source (e.g., LinkedIn) | Deep-dive analysis |
| Position report | View sources for specific position | Position-specific insight |

### Exit Points
| Exit Condition | Destination | User State |
|----------------|-------------|------------|
| Insights gained | Budget planning | Informed decision |
| Poor source identified | Disable/deprioritize source | Optimization |
| Strong source found | Increase investment | Strategic action |

---

## Business Logic

### Metrics Calculated

| Metric | Formula | Purpose |
|--------|---------|---------|
| **Source Conversion Rate** | (Hired / Total Candidates) × 100% | Quality indicator |
| **Cost per Hire** | Total Source Cost / Hires from Source | ROI metric |
| **Time to Hire** | AVG(hired_at - applied_at) per source | Efficiency metric |
| **Offer Acceptance Rate** | (Offers Accepted / Offers Sent) × 100% | Source appeal |

---

## Acceptance Criteria (20 Scenarios)

### Scenario 1: Happy Path - View Source Dashboard

**Type:** ✅ Happy Path

**Given**
- System has candidates from 5 sources:
  - LinkedIn: 50 candidates, 5 hired (10% conversion)
  - Referrals: 20 candidates, 4 hired (20% conversion)
  - Job Boards: 30 candidates, 1 hired (3.3% conversion)
  - Direct: 10 candidates, 2 hired (20% conversion)
  - Career Page: 15 candidates, 1 hired (6.7% conversion)
- Date range: Last 6 months

**When**
- I navigate to "Source Effectiveness" dashboard
- I select date range: Last 6 months

**Then**
- Dashboard displays table:

| Source | Candidates | Hired | Conversion Rate | Avg Time to Hire | Cost per Hire |
|--------|-----------|-------|-----------------|------------------|---------------|
| Referrals | 20 | 4 | 20% 🟢 | 25 days | ฿15,000 |
| Direct | 10 | 2 | 20% 🟢 | 30 days | ฿0 |
| LinkedIn | 50 | 5 | 10% 🟡 | 35 days | ฿25,000 |
| Career Page | 15 | 1 | 6.7% 🟡 | 40 days | ฿5,000 |
| Job Boards | 30 | 1 | 3.3% 🔴 | 45 days | ฿30,000 |

- Color coding: Green ≥15%, Yellow 5-15%, Red <5%
- Chart visualization: Bar chart showing conversion rates
- Insight: "Referrals are your best source - 20% conversion rate"
- Recommendation: "Consider increasing referral bonuses"

---

### Scenario 2: Happy Path - Compare Sources Side-by-Side

**Type:** ✅ Happy Path

**Given**
- Multiple sources tracked

**When**
- I select "LinkedIn" and "Referrals" for comparison

**Then**
- Side-by-side comparison shown:
  ```
  LinkedIn vs. Referrals

  Conversion Rate:  10%     vs.  20%  (Referrals 2× better)
  Time to Hire:     35 days vs.  25 days (Referrals 10 days faster)
  Cost per Hire:    ฿25k    vs.  ฿15k (Referrals ฿10k cheaper)
  
  Winner: Referrals (3/3 metrics better)
  ```
- Actionable insight provided

---

### Scenario 3: Alternative Path - Filter by Position

**Type:** 🔀 Alternative Path

**Given**
- Want to see source effectiveness for "Backend Developer" positions only

**When**
- I filter by position type: "Backend Developer"

**Then**
- Metrics recalculated for backend positions only
- Shows: "LinkedIn performs better for technical roles (15% vs. 10% overall)"
- Position-specific insights help targeted sourcing

---

### Scenario 4: Alternative Path - Time Period Comparison

**Type:** 🔀 Alternative Path

**Given**
- Implemented new sourcing strategy 3 months ago

**When**
- I compare Q1 2026 vs. Q4 2025

**Then**
- Shows trend:
  ```
  Referral Conversion Rate:
  Q4 2025: 12%
  Q1 2026: 20% (+67% improvement)
  
  Insight: Referral program improvements are working
  ```

---

### Scenario 5: Alternative Path - Cost Analysis

**Type:** 🔀 Alternative Path

**Given**
- Budget planning for next quarter

**When**
- I view "Cost per Hire by Source"

**Then**
- Chart shows:
  - Direct: ฿0 (but low volume)
  - Referrals: ฿15,000 (referral bonuses)
  - Career Page: ฿5,000 (marketing)
  - LinkedIn: ฿25,000 (recruiter licenses)
  - Job Boards: ฿30,000 (posting fees)
- ROI calculation: "Referrals: Best ROI at ฿15k per hire with 20% conversion"

---

### Scenario 6: Validation Error - No Data for Period

**Type:** ❌ Validation Error

**Given**
- Select date range: Last 30 days
- No hires in last 30 days

**When**
- Dashboard loads

**Then**
- Warning: "No hires in selected period"
- Suggestion: "Expand date range to see trends"
- Option to view candidates added (even if not hired yet)

---

### Scenario 7: Validation Error - Source Never Used

**Type:** ❌ Validation Error

**Given**
- Source "Twitter" configured but 0 candidates

**When**
- View source effectiveness

**Then**
- Twitter shows: 0 candidates, 0 hired, N/A conversion
- Message: "No candidates from this source yet"
- Hide from main dashboard (avoid clutter)

---

### Scenario 8: Business Rule Error - Incomplete Cost Data

**Type:** ⚠️ Business Rule Error

**Given**
- LinkedIn source has candidates
- Cost per source not configured in system

**When**
- Viewing Cost per Hire

**Then**
- Warning: "Cost data unavailable for LinkedIn"
- Shows other metrics (conversion, time to hire)
- Suggests: "Configure source costs in Settings"

---

### Scenario 9: Permission Denied - Recruiter Limited View

**Type:** 🔒 Permission Denied

**Given**
- I am Recruiter (not HR Manager)
- Cost data is sensitive

**When**
- I view source effectiveness

**Then**
- Can see: Conversion rates, time to hire
- Cannot see: Cost per hire, budget data
- Message: "Cost data available to HR Managers only"

---

### Scenario 10: Loop/Retry - Refresh Metrics

**Type:** 🔄 Loop/Retry

**Given**
- Dashboard loaded yesterday
- New hire completed today

**When**
- I click "Refresh Metrics"

**Then**
- Metrics recalculate with latest data
- Conversion rates update
- Cache cleared
- Real-time accurate data shown

---

### Scenario 11: Empty State - No Hires Yet

**Type:** 📭 Empty State

**Given**
- New recruitment program
- Many candidates but 0 hires yet

**When**
- View source effectiveness

**Then**
- Empty state: "No hires yet to calculate effectiveness"
- Shows partial data: "Candidates by Source"
- Message: "Effectiveness metrics will appear after first hire"

---

### Scenario 12: Session Timeout - Viewing Dashboard

**Type:** ⏰ Timeout

**Given**
- Dashboard open for 45 minutes

**When**
- Session expires

**Then**
- Read-only view continues (public dashboard)
- Filters/date range preserved
- No data loss

---

### Scenario 13: Concurrent Modification - Live Updates

**Type:** ⚡ Concurrent

**Given**
- Viewing dashboard
- Another recruiter hires candidate from LinkedIn

**When**
- Hire completes

**Then**
- Dashboard auto-refreshes (if real-time enabled)
- LinkedIn conversion rate updates: 10% → 10.2%
- Notification: "Metrics updated (new hire)"

---

### Scenario 14: Data Integrity - Outlier Detection

**Type:** ⚠️ Data Integrity

**Given**
- Job Board conversion: 1 hire from 100 candidates (1%)
- Single hire might be statistical anomaly

**When**
- View insights

**Then**
- Warning: "Small sample size - results may not be significant"
- Suggests: "Need at least 20 candidates for reliable metrics"

---

### Scenario 15: Integration Error - Cost API Unavailable

**Type:** ⚠️ Integration Error

**Given**
- External cost tracking API down

**When**
- Loading cost per hire

**Then**
- Other metrics load successfully
- Cost column shows: "Unavailable"
- Graceful degradation

---

### Scenario 16: Alternative Path - Export Report

**Type:** 🔀 Alternative Path

**Given**
- Need to present to executive team

**When**
- I click "Export Report"

**Then**
- PDF generated with:
  - Summary table
  - Visualizations
  - Insights and recommendations
  - Date range and filters applied

---

### Scenario 17: Alternative Path - Drill-Down to Candidates

**Type:** 🔀 Alternative Path

**Given**
- LinkedIn shows 10% conversion

**When**
- I click on LinkedIn row

**Then**
- Shows list of all LinkedIn candidates
- Filtered view: Hired vs. Not Hired
- Can analyze: Why did 90% not convert?

---

### Scenario 18: Loop/Retry - Adjust Source Strategy

**Type:** 🔄 Loop/Retry

**Given**
- Job Boards showing 3% conversion (poor)
- High cost per hire

**When**
- I mark Job Boards as "Low Priority"
- I increase Referral budget

**Then**
- Strategy logged
- Can track impact over next quarter
- Compare before/after metrics

---

### Scenario 19: Data Integrity - Historical Trend

**Type:** ⚠️ Data Integrity

**Given**
- 2 years of historical data

**When**
- View long-term trends

**Then**
- Chart shows: Referral effectiveness declined from 30% to 20%
- Insight: "Referral program needs refresh"
- Trend analysis helps strategic planning

---

### Scenario 20: Performance - Large Dataset

**Type:** ⚠️ Performance

**Given**
- 5,000 candidates across 10 sources
- 2 years of data

**When**
- Load dashboard

**Then**
- Metrics calculate in <2 seconds
- Pagination for detailed views
- Aggregated data cached
- No timeout or lag

---

## Scenario Coverage: ✅ Complete (20 scenarios, all 10 types)

---

## UI/UX Requirements

### Source Effectiveness Dashboard

```
╔═══════════════════════════════════════════════════════════╗
║ Source Effectiveness Report                              ║
╠═══════════════════════════════════════════════════════════╣
║ Date Range: [Last 6 months ▼]   [Export PDF]            ║
║                                                           ║
║ ┌────────────────────────────────────────────────────┐   ║
║ │ Conversion Rate by Source                          │   ║
║ │                                                     │   ║
║ │ Referrals     ████████████████████ 20%            │   ║
║ │ Direct        ████████████████████ 20%            │   ║
║ │ LinkedIn      ██████████ 10%                      │   ║
║ │ Career Page   ███████ 6.7%                        │   ║
║ │ Job Boards    ███ 3.3%                            │   ║
║ └────────────────────────────────────────────────────┘   ║
║                                                           ║
║ Source Details:                                           ║
║ ┌────────────────────────────────────────────────────┐   ║
║ │Source    │Cand.│Hired│Conv%│Avg Days│Cost/Hire  │   ║
║ ├──────────┼─────┼─────┼─────┼────────┼───────────┤   ║
║ │Referrals │  20 │  4  │ 20% │  25    │ ฿15,000   │   ║
║ │Direct    │  10 │  2  │ 20% │  30    │ ฿0        │   ║
║ │LinkedIn  │  50 │  5  │ 10% │  35    │ ฿25,000   │   ║
║ │CareerPage│  15 │  1  │ 7%  │  40    │ ฿5,000    │   ║
║ │Job Boards│  30 │  1  │ 3%  │  45    │ ฿30,000   │   ║
║ └────────────────────────────────────────────────────┘   ║
║                                                           ║
║ 💡 Insights:                                              ║
║ • Referrals are your best source (20% conversion)        ║
║ • Job Boards have poor ROI - consider reducing spend     ║
║ • LinkedIn good for volume, optimize for quality         ║
║                                                           ║
║ [View Trends] [Compare Sources] [Configure Costs]        ║
╚═══════════════════════════════════════════════════════════╝
```

**END OF US-4.11**
