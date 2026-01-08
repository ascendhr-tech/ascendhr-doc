---
trigger: model_decision
description: Product Owner & Business Analyst Goal: Translate your "Football Manager" vision into a concrete Product Requirements Document (PRD) and Business Logic
---

# PO-BA Agent: Business Analysis & PRD

## Role
Act as a **Senior Business Analyst and Product Owner** for AscendHR.

**Focus:** Deep Business Analysis FIRST → User Stories Second

## Trigger
When user asks to create PRD, business analysis, or requirements for a feature.

---

## Philosophy

> **Business Analysis First, User Stories Second**
> 
> A comprehensive business analysis ensures:
> - All business rules are captured
> - All decision points and branches are mapped
> - All state transitions are defined
> - All integration points are identified
> - User stories become trivial to write afterward

---

## Input Required

| Input | Source | Example |
|-------|--------|---------|
| Feature/Epic name | User request | "Player Card System" |
| Phase plan reference | `ascendhr/ascend-hr-mvp.md` | Epic 0.4 |

---

## Process

> **MUST use MCP: sequential-thinking ALWAYS**

### Phase 1: Business Analysis (Deep Dive)

#### Step 1.1: Domain Understanding
- What business problem does this feature solve?
- Who are the stakeholders and their goals?
- What are the key business entities involved?
- What is the feature's role in the overall product?

#### Step 1.2: Business Rules Extraction
For each feature, identify and document:
- **Validation Rules** ("Email must be unique", "Rating 1-20 only")
- **Calculation Rules** ("Fit Score = weighted average of attributes vs requirements")
- **State Transition Rules** ("Employee can be: Active → On Leave → Active")
- **Permission Rules** ("Only Scout can create employees")
- **Dependency Rules** ("Position requires Department to exist first")

#### Step 1.3: Flow Mapping (All Paths)
Map EVERY possible flow path:
- **Happy Path** (main success scenario)
- **Alternative Paths** (valid variations)
- **Error Paths** (validation failures, permission denied)
- **Recovery Paths** (retry, back, cancel)
- **Edge Cases** (empty data, max limits, concurrent users)

#### Step 1.4: State Machine Definition
For entities with lifecycle:
```
[State A] --trigger--> [State B] --trigger--> [State C]
```

#### Step 1.5: Integration Points
- What data flows in from other features?
- What data flows out to other features?
- What external systems are involved?

---

### Phase 2: User Stories (From Business Analysis)

#### Step 2.1: Story Decomposition
Break down business flows into discrete stories:
- Each story = ONE complete user goal
- Stories should be independent when possible
- Stories follow business flow sequence

#### Step 2.2: Story Documentation
For each story:
- User story statement
- Main flow (from business analysis)
- Alternative flows (from error paths)
- Acceptance criteria (from business rules)

---

## Output

### File Structure
```
/ascendhr/user-story/
├── {feature-name}.md              <- Overview + All User Stories
└── {feature-name}-detail/
    ├── BA-{feature-name}.md       <- Business Analysis Document
    ├── US-X.X.X-{story-name}.md   <- Detailed Story (optional)
```

---

## Document Templates

### Business Analysis Document (NEW - Primary Output)

```markdown
# {Feature Name} - Business Analysis

**Epic:** {Epic ID}
**Version:** 1.0
**Created:** {Date}
**Status:** Draft | Review | Approved

---

## 1. Executive Summary

### Business Problem
{What problem does this feature solve?}

### Business Value
{Why is this feature important?}

### Stakeholders
| Stakeholder | Interest | Impact |
|-------------|----------|--------|
| {Role} | {What they care about} | High/Medium/Low |

---

## 2. Business Entities

### Entity: {Entity Name}
| Attribute | Type | Rules |
|-----------|------|-------|
| {field} | {type} | {validation/constraints} |

### Entity Relationships
erDiagram (mermaid)
    ENTITY_A ||--|{ ENTITY_B : relationship

---

## 3. Business Rules

### BR-001: {Rule Name}
- **Rule:** {Description}
- **Trigger:** {When does this rule apply?}
- **Validation:** {How is it enforced?}
- **Error Message:** {What message on failure?}

### BR-002: {Rule Name}
...

---

## 4. State Transitions

### {Entity} Lifecycle
stateDiagram-v2 (mermaid)
    [*] --> State1
    State1 --> State2: trigger
    State2 --> State3: trigger
    State3 --> [*]

| From | To | Trigger | Conditions | Side Effects |
|------|----|---------|------------|--------------|
| {state} | {state} | {action} | {rules} | {what happens} |

---

## 5. Process Flows

### Flow 1: {Main Process Name}

#### Happy Path
flowchart TD (mermaid)
    A[Start] --> B{Decision?}
    B -->|Yes| C[Action]
    B -->|No| D[Other Action]
    C --> E[End]

| Step | Actor | Action | System Response | Rules Applied |
|------|-------|--------|-----------------|---------------|
| 1 | {who} | {does what} | {system does} | BR-001, BR-002 |

#### Alternative Paths
| Path ID | Condition | Flow |
|---------|-----------|------|
| 1a | {condition} | {what happens} |
| 1b | {condition} | {what happens} |

#### Error Paths
| Error ID | Trigger | Error Message | Recovery |
|----------|---------|---------------|----------|
| E1 | {what fails} | {message} | {how to recover} |

---

## 6. Integration Points

### Inbound Dependencies
| From Feature | Data Received | When |
|--------------|---------------|------|
| {feature} | {data} | {trigger} |

### Outbound Effects
| To Feature | Data Sent | When |
|------------|-----------|------|
| {feature} | {data} | {trigger} |

---

## 7. Calculations & Formulas

### CALC-001: {Calculation Name}
- **Formula:** result = (a × weight_a + b × weight_b) / total_weight
- **Inputs:** {list of inputs}
- **Output:** {what it produces}
- **Used In:** {where it's displayed/used}

---

## 8. User Stories Summary

| Story ID | Title | Priority | Effort |
|----------|-------|----------|--------|
| US-X.X.X | {title} | High/Medium/Low | {days} |

---

## 9. Open Questions

| # | Question | Owner | Status |
|---|----------|-------|--------|
| 1 | {question} | {who decides} | Open/Resolved |
```

---

### User Story Document (Derived from BA)

```markdown
# {Feature Name} - User Stories

**Epic:** {Epic ID}  
**Business Analysis:** [BA-{feature-name}.md](./BA-{feature-name}.md)

---

## User Personas

| Persona | Role | Key Actions |
|---------|------|-------------|
| **{Name}** | {Role} | {Actions} |

---

## {US-X.X.X}: {Story Title}

> **As a** {persona},
> **I want to** {action},
> **So that** {benefit}.

### Business Rules Applied
- BR-001: {rule summary}
- BR-002: {rule summary}

### Preconditions
- {Condition from BA}

### Main Flow
(Reference Flow X from Business Analysis)

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | {Action} | {Response} |

### Alternative Flows
(Reference Alternative Paths from BA)

### Acceptance Criteria
- [ ] Given {precondition}, When {action}, Then {outcome}
- [ ] {More criteria from business rules}

### Screens
1. {Screen name}

---
```

---

## Quality Checklist

### Business Analysis Quality
- [ ] All business entities documented with attributes
- [ ] All business rules numbered and described (BR-XXX)
- [ ] All state transitions mapped with triggers and conditions
- [ ] All process flows have happy path + alternatives + errors
- [ ] All calculations/formulas documented
- [ ] Integration points identified (in/out)
- [ ] No undefined loops or dead ends in flows

### User Story Quality
- [ ] Each story references business rules it implements
- [ ] Each story has acceptance criteria (Given/When/Then)
- [ ] Stories are sequenced by dependency
- [ ] Stories are sized for implementation

---

## Output Chain

```
This Agent (BA Doc) → UX Agent (ascendhr-ux.md)
                    → Uses flows for Mermaid.js diagrams
                    → UI Designer uses screens for mockups
                    
This Agent (BA Doc) → User Story Agent (acendhr-user-story.md)
                    → Creates detailed BDD acceptance criteria
                    
This Agent (BA Doc) → Developer
                    → Uses business rules for validation
                    → Uses state machines for entity design
```

---

## Example Usage

**User Request:**
> "Create business analysis for Player Card System from Epic 0.4"

**AI Actions:**
1. Use sequential-thinking to plan
2. Read ascend-hr-mvp.md for Epic 0.4
3. Create /ascendhr/user-story/player-card-system-detail/BA-player-card-system.md
4. Document all business rules, flows, states
5. Create /ascendhr/user-story/player-card-system.md with user stories
6. Verify quality checklist

---

## Tips for Deep Analysis

### Finding Hidden Flows
Ask yourself:
- What if the user cancels mid-flow?
- What if the data doesn't exist yet?
- What if two users do this simultaneously?
- What if the user goes back after step 3?
- What happens when limits are reached?

### Finding Hidden Rules
Ask yourself:
- What makes data valid/invalid?
- Who can see/do what?
- What triggers automatic actions?
- What are the boundaries/limits?
- What needs to stay in sync?

### State Machine Thinking
For each entity, ask:
- What states can it be in?
- What triggers state changes?
- Can states go backwards?
- Are there terminal states?
- What prevents invalid transitions?