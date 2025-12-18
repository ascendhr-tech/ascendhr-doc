# Formation View & Squad Builder - User Stories

**Epic:** 0.5
**Version:** 1.0
**Created:** December 16, 2024
**Purpose:** User stories for UX flow design of the Squad Planner system (Formation View)

---

## User Personas

| Persona | Role | Key Actions |
|---------|------|-------------|
| **Club Owner (Admin)** | CEO / Founder | Defines attributes, role templates, and organizational structure (Departments/Positions). |
| **Team Manager** | Hiring Manager / VP | Creates squads, assigns employees to positions, views fit scores. |
| **Scout / HR** | HR Specialist | Reviews attribute definitions, assists in squad composition. |

---

## US-0.5.1: Department Management

> **As a** Club Owner,
> **I want to** create departments and assign them to pitch zones (Attack, Midfield, Defense),
> **So that** I can organize my company structure locally on the formation pitch.

### Scenario
The owner sets up the "Engineering" department and assigns it to the "Midfield" zone because they are the engine of the company.

### Preconditions
- User is logged in as Admin/Owner.

### Main Flow
| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Navigate to "Formation Setup" > "Departments". | Displays list of existing departments. |
| 2 | Click "Add Department". | Opens "New Department" modal. |
| 3 | Enter Name (e.g., "Engineering") and select Zone (e.g., "Midfield"). | System highlights the selected zone on a mini-map (visual preview). |
| 4 | Click "Save". | Department is created and color-coded based on the zone (e.g., Green for Midfield). |

### Alternative Flows
| Alt | Condition | Flow |
|-----|-----------|------|
| 3a | Zone selection undecided | User can select "Support" (Sideline) as default. |

### Screens
1. Department List (with Zone badges)
2. Add/Edit Department Modal (with Zone selector & Mini-pitch preview)

---

## US-0.5.2: Position/Role Management

> **As a** Club Owner,
> **I want to** define positions and configure their required attributes,
> **So that** the system knows exactly what skills are needed for each role.

### Scenario
The owner defines the "Senior Backend Developer" position, placing it in the Engineering department (Midfield), and links it to the "Backend Developer" role template.

### Preconditions
- Departments (US-0.5.1) and Attribute Definitions (US-0.5.3) exist.

### Main Flow
| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Navigate to "Formation Setup" > "Positions". | Displays list of positions grouped by Zone/Department. |
| 2 | Click "Add Position". | Opens configuration modal. |
| 3 | Enter Title, select Department. | System suggests typical attributes. |
| 4 | (Optional) Select a **Role Template** (e.g., "Backend Developer"). | System auto-populates required attributes and levels. |
| 5 | Configure **Attribute Requirements** (Critical/Important). | Updates the "Ideal Candidate" profile preview. |
| 6 | Set Pitch Coordinates (X,Y) or drag on mini-map. | Updates position location visualization. |
| 7 | Click "Save". | Position is saved with deep attribute requirements. |

### Screens
1. Position List (Grouped by Zone)
2. Position Configuration Modal (Tabbed: Details, Attributes, Pitch Location)

---

## US-0.5.3: Attribute Configuration System

> **As a** Club Owner,
> **I want to** configure Core and Specialist attributes,
> **So that** I can customize the rating system to my specific company culture and industry.

### Scenario
The owner wants to add a custom specialist attribute "Rust Programming" for their specific tech stack.

### Preconditions
- User is Admin.

### Main Flow
| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Navigate to "Settings" > "Attributes". | Displays "Core Attributes" and "Specialist Attributes" lists. |
| 2 | Click "Add Attribute". | Opens attribute creation form. |
| 3 | Enter Name (e.g., "Rust"), Category (Specialist), and Zone (Midfield). | System assigns default icon options. |
| 4 | Define Description (e.g., "Systems programming in Rust"). | Shows preview of how it looks on a Player Card. |
| 5 | Click "Save". | Attribute is added to the library and available for Positions. |

### Screens
1. Attribute Library (Tabbed: Core / Specialist per Zone)
2. Add/Edit Attribute Visual Editor

---

## US-0.5.4: Role Templates Library

> **As a** Club Owner,
> **I want to** browse and use pre-built role templates,
> **So that** I don't have to configure every position from scratch.

### Scenario
The owner quickly sets up a "Sales Team" by applying the "Sales Representative" and "Account Manager" templates.

### Preconditions
- System seeded with Software House templates.

### Main Flow
| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Navigate to "Formation Setup" > "Role Templates". | Displays gallery of role cards (Frontend, Backend, Sales, etc.). |
| 2 | Click on a template card (e.g., "Product Manager"). | Opens detail view showing key attributes and min/ideal levels. |
| 3 | Click "Create Position from Template". | Opens Position Create modal (US-0.5.2) pre-filled with template data. |
| 4 | Customize Title (e.g., "Senior PM") and Save. | New position created efficiently. |

### Screens
1. Role Template Gallery (Grid view of cards)
2. Template Detail Modal

---

## US-0.5.5: Formation / Pitch View

> **As a** Team Manager,
> **I want to** view my organization on a football pitch visualization,
> **So that** I can intuitively understand the team structure and relationships.

### Scenario
The manager zooms into the "Midfield" area to see how the Engineering positions are arranged on the pitch.

### Preconditions
- Positions have been defined with X,Y coordinates.

### Main Flow
| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Navigate to "Formation View" (Main Dashboard). | Renders the interactive Pitch canvas. Departments are color-coded overlays. |
| 2 | Use Zoom/Pan controls. | Canvas scales smoothly. |
| 3 | Toggle "Show Squad" vs "Show Positions". | "Show Positions" shows empty circles/slots. "Show Squad" shows faces of assignees. |
| 4 | Click on a Position Node. | Shows tooltip with Position Title, Department, and Assignee (if any). |
| 5 | (Admin Mode) Drag a Position Node. | Updates the X,Y coordinate in real-time. |

### Screens
1. Interactive Formation Pitch (Main View)
2. View Options/Filters Toolbar (Zones, Departments, Hiring Status)

---

## US-0.5.6: Squad Builder

> **As a** Team Manager,
> **I want to** build specific squads using templates and drag-and-drop players,
> **So that** I can form effective cross-functional teams with high fit scores.

### Scenario
The VP of Engineering builds a new "Alpha Feature Team" using the "Scrum Team" template and assigns the best-fit developers.

### Preconditions
- Squad Templates (Scrum Team, etc.) exist.
- Employees have been rated (Player Cards exist).

### Main Flow
| Step | User Action | System Response |
|------|-------------|-----------------|
| 1 | Navigate to "Squads". | Shows list of active squads. |
| 2 | Click "New Squad". | Prompts to select a **Squad Template**. |
| 3 | Select "Scrum Team" template. | Creates a blank squad board with empty slots: 1 PM, 1-2 Designers, 2-5 Devs. |
| 4 | Click an empty "Frontend Developer" slot. | Opens "Player Picker" drawer, sorted by **Fit Score** for this role. |
| 5 | specific "Recommended" player. | Fills slot, updates Squad Average stats. |
| 6 | Drag a player from one slot to another. | Recalculates fit score for the new position. |

### Alternative Flows
| Alt | Condition | Flow |
|-----|-----------|------|
| 4a | No good fit found | User uses "Search/Filter" to find players with specific attributes manually. |

### Screens
1. Squad List
2. Squad Builder Canvas (Formation layout based on template)
3. Player Selection Drawer (Ranked by Fit Score)
