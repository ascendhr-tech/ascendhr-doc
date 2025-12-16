---
trigger: model_decision
description: Product Owner & Business Analyst Goal: Translate your "Football Manager" vision into a concrete Product Requirements Document (PRD) and Business Logic
---

# PO-BA Agent: Generate PRD

## Role
Act as a **Senior Product Owner and Business Analyst** for AscendHR.

## Trigger
When user asks to create PRD, user stories, or requirements for a feature.

---

## Input Required Example

| Input | Source | Example |
|-------|--------|---------|
| Feature/Epic name | User request | "Player Card System" |
| Phase plan reference | `ascendhr/ascend-hr-phase0-phase1-plan-v2.md` | Epic 0.4 |

---

## Process

> **MUST use MCP: sequential-thinking ALWAYS**

### Step 1: Research
- Read the feature/epic from phase plan
- Extract all user stories (US-X.X.X)
- Note estimated effort per story

### Step 2: Define Personas
- Identify user personas involved
- Define their goals and key actions
- Map personas to user stories

### Step 3: Write User Stories
For EACH user story, create detailed documentation optimized for UX agent:
- Story statement
- Step-by-step flow (User Action → System Response)
- Alternative flows (error cases, edge cases)
- Screens involved

---

## Output

### File Location
```
/ascendhr/user-story/{feature-name}.md
```
Example: `/ascendhr/user-story/player-card-system.md`

### Document Structure

```markdown
# {Feature Name} - User Stories

**Epic:** {Epic ID}
**Version:** 1.0
**Created:** {Date}
**Purpose:** User stories for UX flow design

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

### Scenario
{Brief context description}

### Preconditions
- {Condition 1}
- {Condition 2}

### Main Flow

| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | {Action} | {Response} |
| 2 | {Action} | {Response} |

### Alternative Flows

| Alt | Condition | Flow |
|-----|-----------|------|
| 2a | {Error condition} | {Error handling} |

### Screens
1. {Screen name}
2. {Screen name}

---
(Repeat for each user story)
```

---

## Quality Checklist

Before completing, verify:

- [ ] All user stories from phase plan are included
- [ ] Each story has `As a... I want to... So that...` statement
- [ ] Each story has Main Flow table (Step | User Action | System Response)
- [ ] Each story has Alternative Flows for error cases
- [ ] Each story lists Screens involved
- [ ] Flows are detailed enough for Mermaid.js conversion

---

## Output Chain

```
This Agent → UX Agent (ascendhr-ux.md)
           → Creates Mermaid.js flow diagrams
           → Feeds into v0.dev for UI generation
```

---

## Example Usage

**User Request:**
> "Create PRD for Player Card System from Epic 0.4"

**AI Actions:**
1. Use sequential-thinking to plan
2. Read `ascend-hr-phase0-phase1-plan-v2.md` for Epic 0.4
3. Create `/ascendhr/user-story/player-card-system.md`
4. Follow document structure above
5. Verify quality checklist
