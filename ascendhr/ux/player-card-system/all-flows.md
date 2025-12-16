# Player Card System - UX Flow Diagrams (Combined)

**Source PRD:** `/ascendhr/user-story/player-card-system.md`  
**Purpose:** All Mermaid.js diagrams in one file for easy copy-paste to [mermaid.live](https://mermaid.live)

---

## 00: Site Map

```mermaid
graph TD
    A((Start)) --> B[Login]
    B --> C[Dashboard]
    C --> D[Squad Page]
    
    D --> E[Player Gallery]
    D --> F[Employee List]
    D --> G[Import Wizard]
    
    E --> H[Player Card Detail]
    F --> H
    
    H --> I[Edit Player]
    H --> J[Change Status]
    H --> K[View History]
    
    E --> L[Compare Players]
    
    G --> M[Import Summary]
```

---

## 01: Create Employee + Player Card (US-0.4.1)

```mermaid
graph TD
    A((Start)) --> B[Click Add Employee]
    B --> C[Display Create Form]
    
    subgraph Form["Create Employee Form"]
        C --> D[/Fill Name, Email, Dept, Position/]
        D --> E{Valid?}
        E -->|No| F[Show Field Errors]
        F --> D
        E -->|Yes| G[/Upload Photo - Optional/]
        G --> H{Photo Valid?}
        H -->|Size > 5MB| I[Show Size Error]
        I --> G
        H -->|Yes| J[/Select Reports To/]
    end
    
    subgraph Attributes["Attribute Rating Panel"]
        J --> K[/Rate 10 Attributes 1-20/]
        K --> L[Calculate Current Ability]
        L --> M[/Set Potential Ability/]
        M --> N{Potential >= Current?}
        N -->|No| O[Show Potential Error]
        O --> M
    end
    
    N -->|Yes| P[Click Create Player]
    P --> Q{All Valid?}
    Q -->|No| R[Highlight Errors]
    R --> D
    Q -->|Yes| S[Create Employee Record]
    S --> T[Auto-Create User Account]
    T --> U[Send Invitation Email]
    U --> V[Show Success + Player Card Preview]
    V --> W((End))
```

---

## 02: Employee List & Search (US-0.4.2)

```mermaid
graph TD
    A((Start)) --> B[Navigate to Squad]
    B --> C[Display Employee List]
    
    subgraph List["Employee List"]
        C --> D[/Type in Search Box/]
        D --> E[Filter by Name/Email/ID]
        E --> F{Results Found?}
        F -->|No| G[Show No Results Message]
        G --> D
        F -->|Yes| H[/Apply Filters/]
        H --> I[Filter by Dept/Status/Role]
        I --> J[/Sort by Column/]
        J --> K[Reorder Results]
    end
    
    K --> L[/Click Employee Row/]
    L --> M{Quick Action?}
    M -->|Yes| N[Show Quick Menu]
    N --> O{Select Action}
    O -->|View| P[Go to Player Card]
    O -->|Edit| Q[Go to Edit Mode]
    O -->|Status| R[Open Status Modal]
    M -->|No| P
    
    P --> S((End))
```

---

## 03: View & Update Employee (US-0.4.3)

```mermaid
graph TD
    A((Start)) --> B[Select Employee from List]
    B --> C[Navigate to Player Card]
    
    subgraph View["Player Card Detail - View Mode"]
        C --> D[Display Photo + Info]
        D --> E[Display Radar Chart]
        E --> F[Display Ability Scores]
    end
    
    F --> G[/Click Edit Button/]
    
    subgraph Edit["Player Card Detail - Edit Mode"]
        G --> H[Switch to Edit Mode]
        H --> I[/Update Fields or Attributes/]
        I --> J{Valid Input?}
        J -->|No| K[Show Field Error]
        K --> I
        J -->|Yes| L{Changes Made?}
        L -->|No| M[Save Button Disabled]
        M --> I
    end
    
    L -->|Yes| N[/Click Save Changes/]
    N --> O[Save with Audit Log]
    O --> P[Recalculate Current Ability]
    P --> Q[Show Success Notification]
    Q --> R[Return to View Mode]
    R --> S((End))
```

---

## 04: Change Employment Status (US-0.4.4)

```mermaid
graph TD
    A((Start)) --> B[Click Change Status]
    B --> C[[Open Status Modal]]
    
    subgraph Modal["Status Change Modal"]
        C --> D[/Select New Status/]
        D --> E{Status Type?}
        E -->|On Leave| F[Show Date Fields]
        E -->|Suspended| G[Show Reason Field]
        E -->|Terminated| H[Show Termination Form]
        
        F --> I[/Fill Effective Date/]
        G --> I
        H --> J[/Fill Exit Date + Reason + Handover/]
        J --> I
        
        I --> K{Valid?}
        K -->|No| L[Show Validation Errors]
        L --> I
    end
    
    K -->|Yes| M[/Click Confirm/]
    M --> N[Update Employee Status]
    N --> O[Log to Status History]
    O --> P{Terminated?}
    P -->|Yes| Q[Deactivate User Account]
    Q --> R[Show Confirmation]
    P -->|No| R
    R --> S[Close Modal]
    S --> T((End))
```

---

## 05: Manage Reporting Structure (US-0.4.5)

```mermaid
graph TD
    A((Start)) --> B[Edit Employee Profile]
    B --> C[Show Reports To Field]
    C --> D[/Click Manager Dropdown/]
    D --> E[Display Searchable Manager List]
    E --> F[/Search and Select Manager/]
    
    F --> G{Valid Selection?}
    G -->|Select Self| H[Show Self-Reference Error]
    H --> F
    G -->|Circular Ref| I[Show Circular Error]
    I --> F
    
    G -->|Valid| J[/Click Save/]
    J --> K[Update Hierarchy]
    K --> L[Validate No Circular Ref]
    L --> M[Show Updated Org Info]
    M --> N((End))
```

---

## 06: Bulk Import Employees (US-0.4.6)

```mermaid
graph TD
    A((Start)) --> B[Click Import Employees]
    B --> C[[Open Import Wizard]]
    
    subgraph Step1["Step 1: Template"]
        C --> D[Show Template Section]
        D --> E[/Click Download Template/]
        E --> F[Download CSV File]
    end
    
    subgraph Step2["Step 2: Upload"]
        D --> G[Show Upload Zone]
        F --> G
        G --> H[/Drag-Drop or Select CSV/]
        H --> I{Valid Format?}
        I -->|No| J[Show Format Error]
        J --> H
    end
    
    subgraph Step3["Step 3: Validate"]
        I -->|Yes| K[Parse CSV]
        K --> L[Validate Each Row]
        L --> M[Show Preview Table]
        M --> N[Green = Valid, Red = Invalid]
        N --> O[/Click Row for Error Details/]
    end
    
    subgraph Step4["Step 4: Import"]
        N --> P{All Invalid?}
        P -->|Yes| Q[Disable Import Button]
        Q --> R[Review and Fix Errors]
        R --> H
        
        P -->|No| S[/Click Import Valid Rows/]
        S --> T[Create Employee Records]
        T --> U[Send Invitation Emails]
        U --> V[Show Import Summary]
    end
    
    V --> W[X Created, Y Skipped, Z Errors]
    W --> X((End))
```

---

## 07: Assign Roles (US-0.4.7)

```mermaid
graph TD
    A((Start)) --> B[Edit Employee Profile]
    B --> C[Show Roles Field]
    C --> D[/Click Role Multi-Select/]
    D --> E[Display Available Roles]
    
    E --> F{Permission Check}
    F -->|No Access| G[Role Disabled/Hidden]
    F -->|Has Access| H[/Select or Deselect Roles/]
    
    H --> I[Update Selection]
    I --> J[/Click Save/]
    J --> K[Assign Roles to User]
    K --> L[Update User Permissions]
    L --> M[Log to Audit Trail]
    M --> N((End))
```

---

## 08: View Player Card (US-0.4.8a)

```mermaid
graph TD
    A((Start)) --> B[Navigate to Player Gallery]
    B --> C[Display Card Grid]
    C --> D[/Search or Filter/]
    D --> E[Update Grid]
    E --> F[/Click on Player Card/]
    
    subgraph CardView["Player Card Full View"]
        F --> G[Open Full Card View]
        G --> H[View Photo + Basic Info]
        H --> I[View Radar Chart - 10 Attributes]
        I --> J[View Current vs Potential Ability]
    end
    
    J --> K{View History?}
    K -->|Yes| L[/Click History Tab/]
    L --> M[Display Attribute Timeline]
    K -->|No| N((End))
    M --> N
```

---

## 09: Compare Players (US-0.4.8b)

```mermaid
graph TD
    A((Start)) --> B[Navigate to Player Gallery]
    B --> C[Display Cards with Checkboxes]
    
    subgraph Selection["Player Selection"]
        C --> D[/Select First Player/]
        D --> E[Add to Comparison - Show Badge]
        E --> F[/Select More Players/]
        F --> G{Count Check}
        G -->|Less than 2| H[Compare Button Disabled]
        G -->|2-4 Players| I[Compare Button Enabled]
        G -->|Try 5th| J[Show Max 4 Warning]
        J --> F
    end
    
    I --> K[/Click Compare Selected/]
    K --> L[[Open Comparison Modal]]
    
    subgraph Compare["Comparison Modal"]
        L --> M[Display Side-by-Side Cards]
        M --> N[Show Attribute Comparison]
        N --> O[Highlight Differences]
        O --> P[Green = Higher, Red = Lower]
    end
    
    P --> Q{Export?}
    Q -->|Yes| R[/Click Export/]
    R --> S[Download as Image/PDF]
    Q -->|No| T[/Click Close/]
    S --> T
    T --> U[Return to Gallery]
    U --> V((End))
```

---

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
