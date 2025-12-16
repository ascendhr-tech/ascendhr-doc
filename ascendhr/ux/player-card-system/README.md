# Player Card System - UX Flow Diagrams

**Source PRD:** `/ascendhr/user-story/player-card-system.md`  
**Purpose:** Mermaid.js diagrams for v0.dev UI generation

## Usage

1. Copy `.mmd` file content
2. Paste into [mermaid.live](https://mermaid.live)
3. Export as image
4. Use in v0.dev

## Flow Files

| File | User Story | Description |
|------|------------|-------------|
| `00-site-map.mmd` | - | Navigation structure |
| `01-create-employee.mmd` | US-0.4.1 | Create Employee + Player Card |
| `02-employee-list-search.mmd` | US-0.4.2 | Employee List & Search |
| `03-view-update-employee.mmd` | US-0.4.3 | View & Update Employee |
| `04-change-status.mmd` | US-0.4.4 | Change Employment Status |
| `05-reporting-structure.mmd` | US-0.4.5 | Manage Reporting Structure |
| `06-bulk-import.mmd` | US-0.4.6 | Bulk Import Employees |
| `07-assign-roles.mmd` | US-0.4.7 | Assign Roles |
| `08-view-player-card.mmd` | US-0.4.8a | View Player Card |
| `09-compare-players.mmd` | US-0.4.8b | Compare Players |

## Screen Inventory

| # | Screen | Used In | Components |
|---|--------|---------|------------|
| 1 | Employee List | 01, 02, 03 | DataGrid, Search, Filters |
| 2 | Create Employee Form | 01 | Form, Photo Upload |
| 3 | Attribute Rating Panel | 01, 03 | Sliders, Radar Chart |
| 4 | Filter Panel | 02 | Dropdowns, Range |
| 5 | Quick Actions Menu | 02 | Dropdown |
| 6 | Player Card Detail (View) | 03, 08 | Card, Radar, Tabs |
| 7 | Player Card Detail (Edit) | 03 | Form, Sliders |
| 8 | Status Change Modal | 04 | Modal, Form |
| 9 | Termination Form | 04 | Extended Form |
| 10 | Manager Dropdown | 05 | Searchable Select |
| 11 | Import Wizard | 06 | Steps, Upload, Table |
| 12 | Role Assignment Field | 07 | Multi-select |
| 13 | Player Gallery | 08, 09 | Card Grid, Checkboxes |
| 14 | Comparison Modal | 09 | Side-by-side Cards |

## Component Library

| Component | Description |
|-----------|-------------|
| Player Card | FM-style card with photo, ability, attributes |
| Radar Chart | Spider chart for 10 attributes |
| Attribute Sliders | 1-20 range inputs |
| DataGrid | Sortable, filterable table |
| File Upload | Drag-drop zone |
| Step Wizard | Multi-step indicator |
