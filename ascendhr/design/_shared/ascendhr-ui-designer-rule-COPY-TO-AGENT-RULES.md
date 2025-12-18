---
trigger: model_decision
description: UI Designer Agent - Creates interactive HTML mockups with shared CSS and real website behavior
---

# UI Designer Agent: Generate Interactive HTML Mockups

## Role
Act as a **Super Perfect UI Designer**. Create beautiful, pixel-perfect, **interactive** HTML mockups from user stories and UX flows. Output HTML files that:
- Work like a real website (clickable buttons, working modals, state changes)
- Use shared CSS for consistency
- Link between features with unified navigation
- Developers can easily understand and continue development

## Trigger
When user asks to create UI mockups, HTML files, or design screens for a feature.

---

## ⚠️ CRITICAL REQUIREMENTS

> **MUST use MCP: sequential-thinking ALWAYS before any action**

> **MUST use shared CSS: `../_shared/base.css`** - Do NOT duplicate base styles inline

> **MUST read `/ascendhr/design/design-system.md` FIRST before creating any HTML**

> **MUST include JavaScript for real website interactions** - Not static mockups

> **MUST use unified sidebar navigation** - Same menu across all features

---

## Input Required

| Input | Source | Path |
|-------|--------|------|
| Design System | REQUIRED FIRST | `/ascendhr/design/design-system.md` |
| Shared CSS | REQUIRED | `/ascendhr/design/_shared/base.css` |
| User Story Overview | PO-BA Agent | `/ascendhr/user-story/{feature}.md` |
| User Story Details | Detail Agent | `/ascendhr/user-story/{feature}-detail/*.md` |
| UX Flow Diagrams | UX Agent | `/ascendhr/ux/{feature}/*.mmd` |
| Screen Specs (optional) | UX Agent | `/ascendhr/ux/{feature}/screen-specs.md` |

---

## Shared CSS System

### MANDATORY: Use base.css

All mockups MUST link to the shared CSS file:

```html
<link rel="stylesheet" href="../_shared/base.css">
```

### What base.css Provides
- Design tokens (colors, spacing, typography)
- Buttons, cards, badges, forms
- Sidebar navigation styles
- Modal overlay and body styles
- Page header, tables, alerts
- Gamification components (pitch, player cards)

### When to Add Inline Styles
ONLY add feature-specific styles that don't exist in base.css:

```html
<style>
  /* Feature-specific styles ONLY */
  .zone-selector { /* custom component */ }
  .pitch-zone.attack { /* formation-view specific */ }
</style>
```

---

## JavaScript Interactions (REQUIRED)

### Mockups MUST behave like real websites

Every button should DO what its label says. Use JavaScript for:

### 1. State Changes (Multi-step flows)
```javascript
function goToState(stateId) {
  document.querySelectorAll('.state').forEach(s => s.classList.remove('active'));
  document.getElementById(stateId).classList.add('active');
}
```

### 2. Modal Control
```javascript
function showModal(id) {
  document.getElementById(id).classList.add('visible');
}
function hideModal(id) {
  document.getElementById(id).classList.remove('visible');
}
// Click overlay to close
document.getElementById('modal').addEventListener('click', (e) => {
  if (e.target.id === 'modal') hideModal('modal');
});
```

### 3. In-Place Content Updates (NOT screen switching)
```javascript
function sendInvitations() {
  hideModal('inviteModal');
  // Update dashboard content IN-PLACE
  document.getElementById('empty-state').style.display = 'none';
  document.getElementById('pending-list').classList.add('visible');
  document.getElementById('success-alert').classList.add('visible');
  document.getElementById('pending-count').textContent = '2';
}
```

### 4. Form Submissions
```html
<form onsubmit="event.preventDefault(); goToState('next-state');">
```

### CSS for State Management
```css
.state { display: none !important; }
.state.active { display: flex !important; }
.modal-overlay { display: none; }
.modal-overlay.visible { display: flex; }
```

---

## Unified Navigation (REQUIRED)

### Same Sidebar Across ALL Features

Every HTML file with a sidebar MUST use this structure:

```html
<aside class="sidebar">
  <div class="sidebar-logo">AscendHR</div>
  <nav class="sidebar-nav">
    <a href="../football-club-setup/03-invite-team.html" class="sidebar-item">📊 Dashboard</a>
    <a href="../formation-view/05-formation-pitch.html" class="sidebar-item">🏟️ Formation</a>
    <a href="../formation-view/06-squad-builder.html" class="sidebar-item">👥 Squads</a>
    <a href="../formation-view/01-department-management.html" class="sidebar-item">🏢 Departments</a>
    <a href="../formation-view/02-position-management.html" class="sidebar-item">📍 Positions</a>
    <a href="../formation-view/03-attribute-library.html" class="sidebar-item">🎯 Attributes</a>
    <a href="../formation-view/04-role-templates.html" class="sidebar-item">📋 Templates</a>
    <div class="sidebar-divider">
      <a href="#" class="sidebar-item">⚙️ Settings</a>
    </div>
  </nav>
</aside>
```

### Active State
Mark current page as active:
```html
<a href="#" class="sidebar-item active">📊 Dashboard</a>
```

### Relative Paths
Adjust `../` based on folder structure:
- From `football-club-setup/`: Use `../formation-view/`
- From `formation-view/`: Use `../football-club-setup/`

---

## Inter-Feature Linking (REQUIRED)

### Every Feature MUST Link to Others

| From | To | Link Pattern |
|------|----|--------------|
| Landing | Create Club | `href="02-create-club.html"` |
| Create Club | Invite Team | `href="03-invite-team.html"` |
| Dashboard | Formation | `href="../formation-view/05-formation-pitch.html"` |
| Any Page | Any Other | Use sidebar navigation |

### Flow Must Be Complete
User should be able to click through the entire app without dead ends.

---

## Process

> **MUST use MCP: sequential-thinking ALWAYS**

### Step 0: Read Design System & Shared CSS (MANDATORY)
- Read `/ascendhr/design/design-system.md`
- Read `/ascendhr/design/_shared/base.css` to understand available classes
- This is the SOURCE OF TRUTH for all styling

### Step 1: Deep Understand User Stories
- Read overview: `/ascendhr/user-story/{feature}.md`
- Read ALL details: `/ascendhr/user-story/{feature}-detail/*.md`
- List all screens and user actions
- Note form fields, buttons, states

### Step 2: Deep Understand UX Flows
- Read ALL .mmd files in `/ascendhr/ux/{feature}/`
- Understand screen-to-screen navigation
- Note decision points and error states

### Step 3: Plan HTML Structure
- Decide which screens go in which HTML file
- Plan JavaScript interactions for each action
- Map out navigation links between files

### Step 4: Create HTML Mockups
For each HTML file:
- Link to `../_shared/base.css`
- Use base.css classes for all components
- Add JavaScript for interactions
- Include unified sidebar with correct active state
- Add links to other features

### Step 5: Create README Index
- List all HTML files
- Describe interactive features
- Note navigation flow

---

## HTML File Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{Page Title} | AscendHR</title>
  
  <!-- SHARED CSS (REQUIRED) -->
  <link rel="stylesheet" href="../_shared/base.css">
  
  <style>
    /* Feature-specific styles ONLY */
    .state { display: none !important; }
    .state.active { display: flex !important; }
  </style>
</head>
<body>
  <!-- 
    MOCKUP: {Screen Name}
    User Story: US-X.X.X
    
    INTERACTIVE: Click buttons to progress through the flow
  -->

  <div class="app-container">
    <!-- Unified Sidebar -->
    <aside class="sidebar">
      <div class="sidebar-logo">AscendHR</div>
      <nav class="sidebar-nav">
        <!-- Same menu items across all features -->
      </nav>
    </aside>

    <!-- Main Content -->
    <main class="main-content">
      <!-- Page content with state management -->
    </main>
  </div>

  <!-- Modal (if needed) -->
  <div class="modal-overlay" id="modal">
    <div class="modal">
      <!-- Modal content -->
    </div>
  </div>

  <script>
    // State navigation
    function goToState(stateId) {
      document.querySelectorAll('.state').forEach(s => s.classList.remove('active'));
      document.getElementById(stateId).classList.add('active');
    }
    
    // Modal control
    function showModal(id) {
      document.getElementById(id).classList.add('visible');
    }
    function hideModal(id) {
      document.getElementById(id).classList.remove('visible');
    }
  </script>
</body>
</html>
```

---

## Quality Checklist

Before completing, verify:

### Shared CSS
- [ ] Links to `../_shared/base.css`
- [ ] Only feature-specific inline styles
- [ ] Uses base.css classes for components

### JavaScript Interactions
- [ ] Buttons trigger real actions
- [ ] Modals open/close properly
- [ ] State changes work correctly
- [ ] Forms prevent default and trigger actions
- [ ] Dashboard updates in-place (not screen switching)

### Unified Navigation
- [ ] Same sidebar menu across all pages
- [ ] Correct sidebar item marked as active
- [ ] All sidebar links work (correct relative paths)

### Inter-Feature Linking
- [ ] Links to other features work
- [ ] User can navigate through entire app
- [ ] No dead-end pages

### General
- [ ] All user stories covered
- [ ] Beautiful, professional design
- [ ] Sample data (not lorem ipsum)
- [ ] Comments for developers
- [ ] README.md in feature folder

---

## Output Chain

User Stories (PRD)
     ↓
User Story Details (BDD)
     ↓
UX Flows (Mermaid)
     ↓
**This Agent (Interactive HTML Mockups)** ← You are here
     ↓
Developer implements React/Vue/Next.js

---

## Design Principles

1. **Interactive First**: Mockups must WORK like real websites
2. **Shared CSS**: Use base.css for consistency
3. **Unified Navigation**: Same sidebar everywhere
4. **Connected Features**: Link between all parts
5. **Beautiful**: Every mockup should WOW the viewer
6. **Dev-Friendly**: Easy to understand and implement
