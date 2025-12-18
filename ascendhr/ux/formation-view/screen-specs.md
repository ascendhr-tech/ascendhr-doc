# Screen Specifications

**Feature:** Formation View + Squad Builder
**Total Screens:** 10
**Generated:** December 16, 2024
**Related User Stories:** US-0.5.1 to US-0.5.6

---

## Screen: formation-dashboard
**Name:** Formation Main View
**Layout:** full-width
**Flow:** 00-site-map.mmd

### Components
| Component | Type | Props/Details |
|-----------|------|---------------|
| page-header | heading | h1, text: "Formation View" |
| view-controls | toolbar | Zoom In, Zoom Out, Reset, Filter Zones |
| pitch-canvas | canvas | ID: "pitch-canvas", width: 100%, height: 800px |
| node-tooltip | popover | Hidden by default, shows on hover |
| edit-layout-toggle | switch | label: "Edit Layout" |

### States
| State | Trigger | UI Change |
|-------|---------|-----------|
| hover-node | MouseOver Node | Show tooltip with Title/Dept |
| drag-node | MouseDown + Move | Update Node X,Y position |

---

## Screen: department-list
**Name:** Department Management
**Layout:** list
**Flow:** 01-us-0.5.1-department.mmd

### Components
| Component | Type | Props/Details |
|-----------|------|---------------|
| page-title | heading | text: "Departments" |
| add-btn | button | text: "+ Add Department", variant: primary |
| dept-table | table | cols: Name, Zone, Headcount, Actions |
| zone-badge | badge | color: dynamic (Red=Attack, Green=Midfield) |

---

## Screen: department-modal
**Name:** Add/Edit Department
**Layout:** modal
**Flow:** 01-us-0.5.1-department.mmd

### Form Fields
| Field ID | Label | Type | Required | Options |
|----------|-------|------|----------|---------|
| dept-name | Name | text | Yes | - |
| dept-zone | Zone | radio-group | Yes | Attack, Midfield, Defense, Support |

### Components
| Component | Type | Props/Details |
|-----------|------|---------------|
| zone-preview | image | mini-pitch showing highlighted zone |
| save-btn | button | text: "Save Department" |
| cancel-btn | button | text: "Cancel", variant: secondary |

---

## Screen: position-list
**Name:** Position Management
**Layout:** list
**Flow:** 02-us-0.5.2-position.mmd

### Components
| Component | Type | Props/Details |
|-----------|------|---------------|
| page-title | heading | text: "Positions" |
| add-btn | button | text: "+ Add Position", variant: primary |
| group-header | heading | h3, text: "{Zone Name}" |
| pos-card | card | Title, Dept, Required Attributes count |

---

## Screen: position-modal
**Name:** Add/Edit Position
**Layout:** modal
**Flow:** 02-us-0.5.2-position.mmd

### Components
| Component | Type | Props/Details |
|-----------|------|---------------|
| tabs | tab-group | Details, Attributes, Location |
| template-select | select | label: "Apply Role Template" |
| attr-slider | slider | min: 1, max: 20, label: "{Attribute Name}" |
| importance-select | select | Critical, Important, Nice-to-have |
| mini-map | canvas | Drag marker to set X,Y |

---

## Screen: attribute-library
**Name:** Attribute Configuration
**Layout:** card-grid
**Flow:** 03-us-0.5.3-attribute.mmd

### Components
| Component | Type | Props/Details |
|-----------|------|---------------|
| page-title | heading | text: "Attribute Library" |
| add-attr-btn | button | text: "+ New Attribute" |
| section-core | section | heading: "Core Attributes (Global)" |
| section-spec | section | heading: "Specialist Attributes (By Zone)" |
| attr-card | card | Icon, Name, Description |

---

## Screen: template-gallery
**Name:** Role Templates
**Layout:** card-grid
**Flow:** 04-us-0.5.4-templates.mmd

### Components
| Component | Type | Props/Details |
|-----------|------|---------------|
| page-title | heading | text: "Role Templates" |
| filter-zone | select | All, Attack, Midfield, Defense, Support |
| template-card | card | Role Name, Top 3 Attributes list |
| use-template-btn | button | text: "Use Template" |

---

## Screen: squad-dashboard
**Name:** Squad Dashboard
**Layout:** dashboard
**Flow:** 06-us-0.5.6-squad-builder.mmd

### Components
| Component | Type | Props/Details |
|-----------|------|---------------|
| page-title | heading | text: "My Squads" |
| create-squad-btn | button | text: "+ New Squad" |
| squad-grid | grid | List of active squads |
| squad-card | card | Name, Template, Member fulfillment (e.g. 4/6) |

---

## Screen: squad-builder
**Name:** Squad Builder Board
**Layout:** dashboard
**Flow:** 06-us-0.5.6-squad-builder.mmd

### Components
| Component | Type | Props/Details |
|-----------|------|---------------|
| header | header | Squad Name, Average Fit Score |
| builder-canvas | div | visual layout of slots |
| slot-card | card | Role Title, Assigned Player Face (or Empty) |
| player-drawer | drawer | Hidden by default |
| rec-list | list | Recommended players with Fit % |
| search-input | text | Placeholder: "Search employees..." |

---

## Screen: squad-template-modal
**Name:** Select Squad Template
**Layout:** modal
**Flow:** 06-us-0.5.6-squad-builder.mmd

### Components
| Component | Type | Props/Details |
|-----------|------|---------------|
| template-list | list | Radio select list of templates |
| template-preview | div | Shows roles included (PM, Dev, etc.) |
| squad-name-input | text | Label: "Squad Name" |
| create-btn | button | text: "Start Building" |
