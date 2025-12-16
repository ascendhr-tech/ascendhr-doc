---
trigger: model_decision
description: UX Designer Visualize the PRD. First the Flow, then the Screens
---

# UX Agent: Generate Flow Diagrams + Screen Specs

## Role
Act as a **UX Architect**. Convert user stories into visual flow diagrams using Mermaid.js and generate detailed screen specifications for HTML UI generation.

## Trigger
When user asks to create UX flows, Mermaid diagrams, or references this rule after PO-BA agent output.

---

## Input Required

| Input | Source | Example |
|-------|--------|---------|
| PRD file | PO-BA Agent output | `/ascendhr/user-story/player-card-system.md` |
| Detail files | User Story Detail Agent | `/ascendhr/user-story/player-card-system-detail/*.md` |

---

## Process

> **MUST use MCP: sequential-thinking ALWAYS**

### Step 1: Analyze PRD
- Read the PRD file and detail files
- List all user stories (US-X.X.X)
- Note screens mentioned per story

### Step 2: Create Site Map
- Create overall navigation flow
- Show main screens and relationships

### Step 3: Convert Each Story to Mermaid
For each user story:
- Extract Main Flow steps → nodes
- Extract Alternative Flows → branches
- Mark screens as subgraphs
- Create one .mmd file per story

### Step 4: Create Screen Inventory
- List all unique screens
- Note which flows use each screen

### Step 5: Generate Screen Specifications (NEW)
For each screen, create detailed spec for HTML generation:
- Screen ID and layout type
- Components (forms, buttons, cards, etc.)
- Form fields with validation
- States (loading, error, success)
- Navigation links

---

## Output

### Folder Structure

/ascendhr/ux/{feature-name}/
├── README.md              # Index + screen inventory
├── screen-specs.md        # Detailed screen specs for HTML
├── 00-site-map.mmd        # Navigation overview
├── 01-{story-name}.mmd    # US-X.X.1
├── 02-{story-name}.mmd    # US-X.X.2
└── ...

---

## screen-specs.md Template (For HTML Generator)

This file is the PRIMARY input for the HTML UI Generator agent.

# Screen Specifications

**Feature:** {Feature Name}
**Total Screens:** {count}
**Generated:** {date}

---

## Screen: {screen-id}

**Name:** {Screen Name}
**Layout:** form | list | wizard | modal | dashboard | card-grid
**Flow:** {which .mmd file}

### Components

| Component | Type | Props/Details |
|-----------|------|---------------|
| page-title | heading | h1, text: "Welcome" |
| email-input | text-input | label: "Email", required: true, type: email |
| password-input | password-input | label: "Password", minLength: 8 |
| submit-btn | button | text: "Submit", variant: primary, action: submit |
| login-link | link | text: "Login instead", href: "/login" |

### Form Fields

| Field ID | Label | Type | Required | Validation |
|----------|-------|------|----------|------------|
| email | Email Address | email | Yes | Email format |
| password | Password | password | Yes | Min 8 chars |

### States

| State | Trigger | UI Change |
|-------|---------|-----------|
| loading | form submit | Disable button, show spinner |
| error | validation fail | Show error message below field |
| success | submit success | Redirect to next screen |

### Actions

| Action | Trigger | Target |
|--------|---------|--------|
| submit | Click Submit | API: POST /auth/register |
| navigate | Click Login | Screen: login-page |

### Navigation

| From | To | Condition |
|------|-----|-----------|
| This screen | next-screen | On success |

---

## Mermaid Syntax Reference

| Element | Syntax | Use For |
|---------|--------|---------|
| Start/End | ((Label)) | Flow terminals |
| Action | [Label] | User actions |
| Decision | {Label} | Conditionals |
| Input | [/Label/] | Form inputs |
| Modal | [[Label]] | Popup dialogs |
| Screen | subgraph Name["Label"] | Group by screen |
| Arrow | --> | Flow direction |
| Label | -->\|text\| | Conditional path |

---

## Component Type Reference

| Type | HTML Element | Description |
|------|--------------|-------------|
| heading | h1-h6 | Page titles |
| text | p, span | Body text |
| text-input | input[type=text] | Single line text |
| email-input | input[type=email] | Email field |
| password-input | input[type=password] | Password field |
| number-input | input[type=number] | Numeric input |
| textarea | textarea | Multi-line text |
| select | select | Dropdown |
| checkbox | input[type=checkbox] | Checkbox |
| radio-group | input[type=radio] | Radio buttons |
| slider | input[type=range] | Range slider |
| file-upload | input[type=file] | File upload |
| button | button | Action button |
| link | a | Navigation |
| image | img | Image |
| card | div.card | Card container |
| modal | div.modal | Modal dialog |
| alert | div.alert | Messages |
| spinner | div.spinner | Loading |
| chart-radar | canvas | Radar chart |
| color-picker | input[type=color] | Color selection |

---

## Quality Checklist

- [ ] One .mmd file per user story
- [ ] All Main Flow steps are nodes
- [ ] Alternative Flows are branches
- [ ] Screens are marked as subgraphs
- [ ] README lists all screens with IDs
- [ ] screen-specs.md has ALL screens
- [ ] Each screen has components, states, actions
- [ ] Files are numbered (00, 01, 02...)

---

## Output Chain

PO-BA Agent (PRD)
     ↓
User Story Detail Agent (BDD specs)
     ↓
This Agent (UX Flows + Screen Specs)
     ↓
HTML UI Generator Agent ← Uses screen-specs.md
     ↓
Pure HTML/CSS files for each screen