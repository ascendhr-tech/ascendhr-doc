# Player Card Calculation Logic (v2)

> **Purpose:** Complete calculation formulas for Player Card system with dynamic attribute system.  
> **For:** Dev team implementation and Excel conversion.  
> **Reference:** US-0.4.1, US-0.4.3, US-0.4.8a, US-0.5.2, US-0.5.3

---

## 1. System Overview

The Player Card system uses a **dynamic attribute system** where:
- **Attributes** are defined in a library with weights (Low/Medium/High)
- **Positions** select which attributes they require with priorities (Critical/Important/Nice-to-have)
- **Players** are rated on attributes assigned to their position

---

## 2. Attribute Library Configuration

### 2.1 Attribute Categories
| Category | Examples |
|----------|----------|
| Core (Soft Skills) | Leadership, Teamwork, Communication, Adaptability, Determination |
| Technical | Coding, System Design, Problem Solving, Visual Design, UX Thinking, Data Analysis |
| Business | Negotiation, Closing, Client Relations, Sales, Strategic Thinking |
| Creative | Creativity, Prototyping, Design Thinking |

### 2.2 Attribute Weight Multipliers
Each attribute in the library has a weight that affects **Overall Score** calculation:

| Weight | Multiplier | Use Case |
|--------|------------|----------|
| Low | ×1.0 | Bonus/supplementary skills |
| Medium | ×1.25 | Standard importance skills |
| High | ×1.5 | Critical core competencies |

### 2.3 Scale Definition (1-20)
| Range | Level | Color | Description |
|-------|-------|-------|-------------|
| 1-5 | Low | 🔴 Red | Needs significant improvement |
| 6-10 | Developing | 🟡 Yellow | Learning, needs guidance |
| 11-15 | Proficient | 🟢 Green | Competent, meets expectations |
| 16-20 | Exceptional | 🔵 Blue | Mastery level |

**Excel Formula (Scale Classification):**
```excel
=IF(A1<=5,"Low",IF(A1<=10,"Developing",IF(A1<=15,"Proficient","Exceptional")))
```

---

## 3. Position Attribute Requirements

Each position defines its required attributes with:

### 3.1 Priority Weights
| Priority | Stars | Multiplier | Description |
|----------|-------|------------|-------------|
| Critical | ★★★ | ×3.0 | Must match closely |
| Important | ★★ | ×2.0 | Should match |
| Nice-to-have | ★ | ×1.0 | Bonus points if match |

### 3.2 Minimum Required Value
Each attribute has a minimum threshold (e.g., 15+, 12+, 10+).

### 3.3 Example: Senior Backend Developer
| Attribute | Priority | Min Value | Priority Weight |
|-----------|----------|-----------|-----------------|
| Coding | Critical ★★★ | 15 | 3.0 |
| System Design | Critical ★★★ | 13 | 3.0 |
| Teamwork | Critical ★★★ | 14 | 3.0 |
| Leadership | Important ★★ | 12 | 2.0 |
| Problem Solving | Important ★★ | 12 | 2.0 |
| Communication | Nice-to-have ★ | 10 | 1.0 |

---

## 4. Calculation Formulas

### 4.1 Overall Score (0-100)

Uses **ALL player attributes**, weighted by library attribute weight.

**Formula:**
```
weighted_sum = Σ(attribute_value × attribute_weight_multiplier)
weight_total = Σ(attribute_weight_multiplier)
raw_average = weighted_sum / weight_total
overall_score = raw_average × 5
```

**Example:**
| Attribute | Value | Library Weight | Multiplier | Weighted Value |
|-----------|-------|----------------|------------|----------------|
| Coding | 17 | High | 1.5 | 25.5 |
| System Design | 15 | High | 1.5 | 22.5 |
| Leadership | 14 | High | 1.5 | 21.0 |
| Teamwork | 16 | High | 1.5 | 24.0 |
| Communication | 13 | Medium | 1.25 | 16.25 |
| Problem Solving | 15 | Medium | 1.25 | 18.75 |
| Adaptability | 12 | Medium | 1.25 | 15.0 |
| Creativity | 11 | Low | 1.0 | 11.0 |
| **Totals** | | | **11.25** | **154.0** |

Calculation:
- Raw Average = 154.0 / 11.25 = 13.69
- Overall Score = 13.69 × 5 = **68.4 ≈ 68**

**Excel Formula:**
```excel
=ROUND(SUMPRODUCT(AttributeValues, WeightMultipliers) / SUM(WeightMultipliers) * 5, 0)
```

### 4.2 Player Tier
| Tier | Overall Score | Card Style |
|------|---------------|------------|
| 🥇 Gold | 90+ | Gold border/glow |
| 🥈 Silver | 80-89 | Silver border |
| 🥉 Bronze | < 80 | Bronze border |

---

### 4.3 Position Fit Score (0-100%)

Uses **ONLY position's required attributes**, weighted by priority.

**Step 1: Calculate Individual Attribute Score**

For each required attribute:
| Condition | Classification | Score |
|-----------|----------------|-------|
| Actual ≥ Min + 2 | **Exceeds** | 100 |
| Actual ≥ Min - 1 | **Meets** | 100 |
| Actual < Min - 1 | **Below** | max(0, 100 - gap × 15) |

Where: `gap = min_value - actual`

**Step 2: Apply Priority Weights**
```
weighted_score = attribute_score × priority_weight
```

**Step 3: Calculate Final Fit Score**
```
fit_score = Σ(weighted_score) / Σ(priority_weight)
```

**Example: Player vs Senior Backend Developer**
| Attribute | Actual | Min Req | Gap | Class | Score | Priority | Weight | Weighted |
|-----------|--------|---------|-----|-------|-------|----------|--------|----------|
| Coding | 17 | 15 | +2 | Exceeds | 100 | ★★★ | 3 | 300 |
| System Design | 15 | 13 | +2 | Exceeds | 100 | ★★★ | 3 | 300 |
| Teamwork | 14 | 14 | 0 | Meets | 100 | ★★★ | 3 | 300 |
| Leadership | 14 | 12 | +2 | Exceeds | 100 | ★★ | 2 | 200 |
| Problem Solving | 10 | 12 | -2 | Below | 70 | ★★ | 2 | 140 |
| Communication | 13 | 10 | +3 | Exceeds | 100 | ★ | 1 | 100 |
| **Totals** | | | | | | | **14** | **1340** |

Calculation:
- Fit Score = 1340 / 14 = **95.7% ≈ 96%**

**Excel Formulas:**

Attribute Score:
```excel
=IF(Actual >= MinReq + 2, 100, IF(Actual >= MinReq - 1, 100, MAX(0, 100 - (MinReq - Actual) * 15)))
```

Fit Score:
```excel
=SUMPRODUCT(AttributeScores, PriorityWeights) / SUM(PriorityWeights)
```

---

### 4.4 Gap Analysis

For each required attribute:
| Classification | Condition | Display |
|----------------|-----------|---------|
| Exceeds | Actual ≥ Min + 2 | ▲ Green (+N) |
| Meets | Min - 1 ≤ Actual < Min + 2 | — Gray |
| Below | Actual < Min - 1 | ▼ Red (-N) |

**Summary Counts:**
- Count(Exceeds), Count(Meets), Count(Below)

---

### 4.5 Fit Score Color Coding
| Fit Score | Rating | Color |
|-----------|--------|-------|
| 90-100% | Excellent | Green `#22c55e` |
| 70-89% | Good | Blue `#3b82f6` |
| 50-69% | Fair | Amber `#f59e0b` |
| 0-49% | Poor | Red `#ef4444` |

---

## 5. Complete Example: Low Fit Score

### Player: New Hire for Product Manager Role

**Product Manager Requirements:**
| Attribute | Min | Priority |
|-----------|-----|----------|
| Leadership | 15 | ★★★ (3) |
| Communication | 16 | ★★★ (3) |
| Strategic Thinking | 14 | ★★★ (3) |
| Negotiation | 12 | ★★ (2) |
| Problem Solving | 14 | ★★ (2) |
| Teamwork | 12 | ★ (1) |

**New Hire Actuals:**
| Attribute | Actual | Min | Gap | Class | Score | Wgt | Weighted |
|-----------|--------|-----|-----|-------|-------|-----|----------|
| Leadership | 8 | 15 | -7 | Below | 0 | 3 | 0 |
| Communication | 12 | 16 | -4 | Below | 40 | 3 | 120 |
| Strategic Thinking | 10 | 14 | -4 | Below | 40 | 3 | 120 |
| Negotiation | 11 | 12 | -1 | Meets | 100 | 2 | 200 |
| Problem Solving | 10 | 14 | -4 | Below | 40 | 2 | 80 |
| Teamwork | 14 | 12 | +2 | Exceeds | 100 | 1 | 100 |
| **Total** | | | | | | **14** | **620** |

- Fit Score = 620 / 14 = **44.3% (Poor - Red)**
- Gap Summary: 1 Exceeds, 1 Meets, 4 Below

---

## 6. Data Models

### 6.1 Attribute (Library)
```json
{
  "id": "uuid",
  "name": "Leadership",
  "category": "core",
  "weight": "high",
  "weight_multiplier": 1.5
}
```

### 6.2 Position Requirement
```json
{
  "position_id": "uuid",
  "attributes": [
    { "attr_id": "leadership", "priority": "critical", "priority_weight": 3, "min_value": 15 },
    { "attr_id": "communication", "priority": "important", "priority_weight": 2, "min_value": 12 }
  ]
}
```

### 6.3 Player Attributes
```json
{
  "employee_id": "uuid",
  "ratings": [
    { "attr_id": "leadership", "value": 17 },
    { "attr_id": "communication", "value": 15 }
  ]
}
```

---

## 7. Summary of All Formulas

| Metric | Formula | Range |
|--------|---------|-------|
| **Attribute Weight Multiplier** | low=1.0, medium=1.25, high=1.5 | - |
| **Position Priority Weight** | nice-to-have=1, important=2, critical=3 | - |
| **Overall Score** | `Σ(value × attr_weight) / Σ(attr_weight) × 5` | 0-100 |
| **Player Tier** | ≥90 Gold, ≥80 Silver, <80 Bronze | - |
| **Attribute Score (Exceeds)** | actual ≥ min + 2 → 100 | 100 |
| **Attribute Score (Meets)** | actual ≥ min - 1 → 100 | 100 |
| **Attribute Score (Below)** | `max(0, 100 - (min - actual) × 15)` | 0-100 |
| **Position Fit Score** | `Σ(score × priority_weight) / Σ(priority_weight)` | 0-100% |
| **Scale Level** | ≤5 Low, ≤10 Developing, ≤15 Proficient, >15 Exceptional | - |

---

## 8. Key Differences from v1

| Aspect | v1 (Old) | v2 (Correct) |
|--------|----------|--------------|
| Attributes | Fixed 8 attributes | Dynamic from library (18+) |
| Overall Score | Simple average × 5 | Weighted average × 5 |
| Fit Score Attributes | Fixed 5 core | Position-specific requirements |
| Fit Score Weights | Equal weight | Priority-based (1/2/3) |
| Position Requirements | Hardcoded table | Configurable per position |

---

**Document Version:** 2.0  
**Created:** 2024-12-25  
**Based On:** User Stories US-0.4.x, US-0.5.2, US-0.5.3
