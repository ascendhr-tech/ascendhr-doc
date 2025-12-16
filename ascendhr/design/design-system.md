# AscendHR Design System

> Professional HRM design system built with **TailwindCSS** + **shadcn/ui**. This document is optimized for AI agents to generate consistent HTML mockups.

---

## Quick Reference

| Element | Color | Radius | Shadow |
|---------|-------|--------|--------|
| Button Primary | `#3B82F6` | 8px | soft |
| Button Secondary | `#F1F5F9` | 8px | none |
| Card | `#FFFFFF` | 12px | soft |
| Badge | varies | 9999px | none |
| Input | `#FFFFFF` | 8px | none |
| Background | `#F8FAFC` | - | - |

---

## 1. Design Tokens (CSS Variables)

```css
:root {
  /* === COLORS === */
  --primary: #3B82F6;
  --primary-light: #EFF6FF;
  --primary-dark: #1E40AF;
  --secondary: #F1F5F9;
  --secondary-foreground: #334155;
  --accent: #22C55E;
  --accent-light: #F0FDF4;
  --destructive: #EF4444;
  --warning: #FACC15;
  --muted: #F1F5F9;
  --muted-foreground: #64748B;
  --background: #FFFFFF;
  --foreground: #334155;
  --border: #E2E8F0;
  --card: #FFFFFF;
  --white: #FFFFFF;

  /* === GRADIENTS === */
  --gradient-primary: linear-gradient(135deg, #3B82F6, #7C3AED);
  --gradient-hero: linear-gradient(135deg, #3B82F6 0%, #7C3AED 100%);
  --gradient-card: linear-gradient(145deg, #FFFFFF 0%, #F8FAFC 100%);

  /* === SHADOWS === */
  --shadow-soft: 0 2px 8px -2px rgba(51, 65, 85, 0.08);
  --shadow-medium: 0 4px 16px -4px rgba(51, 65, 85, 0.12);
  --shadow-strong: 0 8px 32px -8px rgba(51, 65, 85, 0.16);

  /* === RADIUS === */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-full: 9999px;

  /* === SPACING === */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 20px;
  --space-6: 24px;
  --space-8: 32px;

  /* === TYPOGRAPHY === */
  --font-sans: system-ui, -apple-system, sans-serif;
  --font-size-xs: 12px;
  --font-size-sm: 14px;
  --font-size-base: 16px;
  --font-size-lg: 18px;
  --font-size-xl: 20px;
  --font-size-2xl: 24px;
  --font-size-3xl: 30px;
  --font-weight-normal: 400;
  --font-weight-medium: 500;
  --font-weight-semibold: 600;
  --font-weight-bold: 700;
}

/* === DARK MODE === */
.dark {
  --background: #0F172A;
  --foreground: #F1F5F9;
  --card: #1E293B;
  --border: #334155;
  --muted: #334155;
  --muted-foreground: #94A3B8;
  --primary-light: #1E3A5F;
}

/* === BASE RESET === */
* { box-sizing: border-box; margin: 0; padding: 0; }
body { 
  font-family: var(--font-sans); 
  font-size: var(--font-size-base);
  line-height: 1.5;
  color: var(--foreground); 
  background: var(--background); 
}
```

---

## 2. Color Palette

### Light Mode

| Token | Hex | Usage |
|-------|-----|-------|
| `primary` | `#3B82F6` | Primary actions, links, focus |
| `primary-light` | `#EFF6FF` | Light primary backgrounds |
| `primary-dark` | `#1E40AF` | Hover states |
| `secondary` | `#F1F5F9` | Secondary buttons |
| `accent` | `#22C55E` | Success states |
| `destructive` | `#EF4444` | Errors, delete |
| `warning` | `#FACC15` | Warnings |
| `muted-foreground` | `#64748B` | Secondary text |
| `foreground` | `#334155` | Primary text |
| `border` | `#E2E8F0` | Borders, dividers |
| `background` | `#FFFFFF` | Page background |

### Dark Mode

| Token | Hex |
|-------|-----|
| `background` | `#0F172A` |
| `foreground` | `#F1F5F9` |
| `card` | `#1E293B` |
| `border` | `#334155` |

---

## 3. HTML Components

### Buttons

```html
<!-- Primary Button -->
<button style="
  background: #3B82F6;
  color: white;
  border: none;
  padding: 10px 16px;
  font-size: 14px;
  font-weight: 500;
  border-radius: 8px;
  cursor: pointer;
  box-shadow: 0 2px 8px -2px rgba(51,65,85,0.08);
">Primary</button>

<!-- Secondary Button -->
<button style="
  background: #F1F5F9;
  color: #334155;
  border: none;
  padding: 10px 16px;
  font-size: 14px;
  font-weight: 500;
  border-radius: 8px;
  cursor: pointer;
">Secondary</button>

<!-- Destructive Button -->
<button style="
  background: #EF4444;
  color: white;
  border: none;
  padding: 10px 16px;
  font-size: 14px;
  font-weight: 500;
  border-radius: 8px;
  cursor: pointer;
">Delete</button>

<!-- Outline Button -->
<button style="
  background: transparent;
  color: #334155;
  border: 1px solid #E2E8F0;
  padding: 10px 16px;
  font-size: 14px;
  font-weight: 500;
  border-radius: 8px;
  cursor: pointer;
">Outline</button>

<!-- Gradient/Hero Button -->
<button style="
  background: linear-gradient(135deg, #3B82F6, #7C3AED);
  color: white;
  border: none;
  padding: 12px 24px;
  font-size: 14px;
  font-weight: 500;
  border-radius: 8px;
  cursor: pointer;
  box-shadow: 0 4px 16px -4px rgba(51,65,85,0.12);
">Get Started</button>
```

### Badges

```html
<!-- Default Badge -->
<span style="display: inline-flex; background: #3B82F6; color: white; padding: 2px 10px; font-size: 12px; font-weight: 600; border-radius: 9999px;">Active</span>

<!-- Success Badge -->
<span style="display: inline-flex; background: #22C55E; color: white; padding: 2px 10px; font-size: 12px; font-weight: 600; border-radius: 9999px;">Approved</span>

<!-- Warning Badge -->
<span style="display: inline-flex; background: #FACC15; color: #713F12; padding: 2px 10px; font-size: 12px; font-weight: 600; border-radius: 9999px;">Pending</span>

<!-- Destructive Badge -->
<span style="display: inline-flex; background: #EF4444; color: white; padding: 2px 10px; font-size: 12px; font-weight: 600; border-radius: 9999px;">Rejected</span>
```

### Cards

```html
<!-- Basic Card -->
<div style="
  background: white;
  border: 1px solid #E2E8F0;
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 2px 8px -2px rgba(51,65,85,0.08);
">
  <h3 style="font-size: 24px; font-weight: 600; margin-bottom: 8px;">Card Title</h3>
  <p style="color: #64748B; font-size: 14px;">Card description goes here.</p>
</div>

<!-- Stat Card -->
<div style="
  background: white;
  border: 1px solid #E2E8F0;
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 2px 8px -2px rgba(51,65,85,0.08);
">
  <p style="color: #64748B; font-size: 14px; margin-bottom: 4px;">Total Employees</p>
  <p style="font-size: 30px; font-weight: 700; color: #334155;">1,234</p>
  <p style="color: #22C55E; font-size: 12px; margin-top: 8px;">↑ 12% from last month</p>
</div>
```

### Form Inputs

```html
<!-- Text Input -->
<input type="text" placeholder="Enter text..." style="
  width: 100%;
  padding: 10px 12px;
  font-size: 14px;
  border: 1px solid #E2E8F0;
  border-radius: 8px;
  outline: none;
  background: white;
  color: #334155;
">

<!-- Input with Label -->
<div style="margin-bottom: 16px;">
  <label style="display: block; font-size: 14px; font-weight: 500; margin-bottom: 6px; color: #334155;">Email</label>
  <input type="email" placeholder="you@example.com" style="
    width: 100%;
    padding: 10px 12px;
    font-size: 14px;
    border: 1px solid #E2E8F0;
    border-radius: 8px;
    outline: none;
  ">
</div>

<!-- Select Dropdown -->
<select style="
  width: 100%;
  padding: 10px 12px;
  font-size: 14px;
  border: 1px solid #E2E8F0;
  border-radius: 8px;
  background: white;
  color: #334155;
  cursor: pointer;
">
  <option>Select option...</option>
  <option>Option 1</option>
  <option>Option 2</option>
</select>
```

### Tables

```html
<table style="width: 100%; border-collapse: collapse; font-size: 14px;">
  <thead>
    <tr style="border-bottom: 1px solid #E2E8F0;">
      <th style="text-align: left; padding: 12px; font-weight: 500; color: #64748B;">Name</th>
      <th style="text-align: left; padding: 12px; font-weight: 500; color: #64748B;">Role</th>
      <th style="text-align: left; padding: 12px; font-weight: 500; color: #64748B;">Status</th>
    </tr>
  </thead>
  <tbody>
    <tr style="border-bottom: 1px solid #E2E8F0;">
      <td style="padding: 12px; color: #334155;">John Doe</td>
      <td style="padding: 12px; color: #64748B;">Developer</td>
      <td style="padding: 12px;">
        <span style="background: #22C55E; color: white; padding: 2px 10px; font-size: 12px; font-weight: 600; border-radius: 9999px;">Active</span>
      </td>
    </tr>
  </tbody>
</table>
```

### Avatars

```html
<!-- Avatar with Initials -->
<div style="
  width: 40px;
  height: 40px;
  background: #3B82F6;
  color: white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 14px;
  font-weight: 600;
">JD</div>

<!-- Avatar with Image -->
<img src="https://i.pravatar.cc/40" style="width: 40px; height: 40px; border-radius: 50%; object-fit: cover;">
```

### Alerts

```html
<!-- Info Alert -->
<div style="background: #EFF6FF; border: 1px solid #3B82F6; border-radius: 8px; padding: 16px; color: #1E40AF; font-size: 14px;">
  ℹ️ This is an informational message.
</div>

<!-- Success Alert -->
<div style="background: #F0FDF4; border: 1px solid #22C55E; border-radius: 8px; padding: 16px; color: #166534; font-size: 14px;">
  ✓ Operation completed successfully!
</div>

<!-- Warning Alert -->
<div style="background: #FFFBEB; border: 1px solid #FACC15; border-radius: 8px; padding: 16px; color: #713F12; font-size: 14px;">
  ⚠️ Please review before proceeding.
</div>

<!-- Error Alert -->
<div style="background: #FEF2F2; border: 1px solid #EF4444; border-radius: 8px; padding: 16px; color: #991B1B; font-size: 14px;">
  ✕ An error occurred. Please try again.
</div>
```

### Progress Bar

```html
<div style="background: #E2E8F0; border-radius: 9999px; height: 8px; width: 100%;">
  <div style="background: #3B82F6; border-radius: 9999px; height: 8px; width: 65%;"></div>
</div>
```

### Checkbox

```html
<label style="display: flex; align-items: center; gap: 8px; cursor: pointer; font-size: 14px;">
  <input type="checkbox" style="width: 16px; height: 16px; accent-color: #3B82F6;">
  <span>I agree to the terms</span>
</label>
```

---

## 4. Page Templates

### Dashboard Layout

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dashboard | AscendHR</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: system-ui, -apple-system, sans-serif; background: #F8FAFC; color: #334155; }
    
    .sidebar { position: fixed; left: 0; top: 0; width: 260px; height: 100vh; background: #FAFAFA; border-right: 1px solid #E2E8F0; padding: 20px; }
    .sidebar-logo { font-size: 20px; font-weight: 700; color: #3B82F6; margin-bottom: 32px; }
    .sidebar-nav { display: flex; flex-direction: column; gap: 4px; }
    .sidebar-item { padding: 10px 12px; border-radius: 8px; color: #64748B; text-decoration: none; font-size: 14px; display: flex; align-items: center; gap: 10px; }
    .sidebar-item:hover { background: #F1F5F9; color: #334155; }
    .sidebar-item.active { background: #EFF6FF; color: #3B82F6; font-weight: 500; }
    
    .main { margin-left: 260px; padding: 32px; }
    .header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 32px; }
    .header-title { font-size: 24px; font-weight: 600; }
    
    .stats-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 20px; margin-bottom: 32px; }
    .stat-card { background: white; border: 1px solid #E2E8F0; border-radius: 12px; padding: 24px; box-shadow: 0 2px 8px -2px rgba(51,65,85,0.08); }
    .stat-label { font-size: 14px; color: #64748B; margin-bottom: 4px; }
    .stat-value { font-size: 30px; font-weight: 700; }
    .stat-change { font-size: 12px; margin-top: 8px; }
    .stat-change.positive { color: #22C55E; }
    .stat-change.negative { color: #EF4444; }
    
    .content-card { background: white; border: 1px solid #E2E8F0; border-radius: 12px; padding: 24px; box-shadow: 0 2px 8px -2px rgba(51,65,85,0.08); }
    .content-title { font-size: 18px; font-weight: 600; margin-bottom: 16px; }
    
    .btn-primary { background: #3B82F6; color: white; border: none; padding: 10px 16px; font-size: 14px; font-weight: 500; border-radius: 8px; cursor: pointer; }
  </style>
</head>
<body>
  <aside class="sidebar">
    <div class="sidebar-logo">AscendHR</div>
    <nav class="sidebar-nav">
      <a href="#" class="sidebar-item active">📊 Dashboard</a>
      <a href="#" class="sidebar-item">👥 Employees</a>
      <a href="#" class="sidebar-item">📅 Leave</a>
      <a href="#" class="sidebar-item">💰 Payroll</a>
      <a href="#" class="sidebar-item">📋 Recruitment</a>
      <a href="#" class="sidebar-item">⚙️ Settings</a>
    </nav>
  </aside>

  <main class="main">
    <header class="header">
      <h1 class="header-title">Dashboard</h1>
      <button class="btn-primary">+ New Employee</button>
    </header>

    <div class="stats-grid">
      <div class="stat-card">
        <p class="stat-label">Total Employees</p>
        <p class="stat-value">1,234</p>
        <p class="stat-change positive">↑ 12% from last month</p>
      </div>
      <div class="stat-card">
        <p class="stat-label">On Leave Today</p>
        <p class="stat-value">23</p>
        <p class="stat-change negative">↓ 5% from yesterday</p>
      </div>
      <div class="stat-card">
        <p class="stat-label">Open Positions</p>
        <p class="stat-value">8</p>
        <p class="stat-change positive">↑ 2 new this week</p>
      </div>
      <div class="stat-card">
        <p class="stat-label">Pending Approvals</p>
        <p class="stat-value">15</p>
        <p class="stat-change">Awaiting action</p>
      </div>
    </div>

    <div class="content-card">
      <h2 class="content-title">Recent Activity</h2>
      <p style="color: #64748B;">Content goes here...</p>
    </div>
  </main>
</body>
</html>
```

### Login Page

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Login | AscendHR</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: system-ui, -apple-system, sans-serif; background: linear-gradient(135deg, #3B82F6 0%, #7C3AED 100%); min-height: 100vh; display: flex; align-items: center; justify-content: center; }
    
    .login-card { background: white; border-radius: 16px; padding: 48px; width: 100%; max-width: 420px; box-shadow: 0 8px 32px -8px rgba(0,0,0,0.2); }
    .login-logo { font-size: 28px; font-weight: 700; color: #3B82F6; text-align: center; margin-bottom: 8px; }
    .login-subtitle { text-align: center; color: #64748B; font-size: 14px; margin-bottom: 32px; }
    
    .form-group { margin-bottom: 20px; }
    .form-label { display: block; font-size: 14px; font-weight: 500; margin-bottom: 6px; color: #334155; }
    .form-input { width: 100%; padding: 12px; font-size: 14px; border: 1px solid #E2E8F0; border-radius: 8px; outline: none; }
    .form-input:focus { border-color: #3B82F6; box-shadow: 0 0 0 3px rgba(59,130,246,0.1); }
    
    .login-btn { width: 100%; background: linear-gradient(135deg, #3B82F6, #7C3AED); color: white; border: none; padding: 14px; font-size: 16px; font-weight: 600; border-radius: 8px; cursor: pointer; margin-top: 8px; }
    
    .login-footer { text-align: center; margin-top: 24px; font-size: 14px; color: #64748B; }
    .login-footer a { color: #3B82F6; text-decoration: none; }
  </style>
</head>
<body>
  <div class="login-card">
    <h1 class="login-logo">AscendHR</h1>
    <p class="login-subtitle">Sign in to your account</p>
    
    <form>
      <div class="form-group">
        <label class="form-label">Email</label>
        <input type="email" class="form-input" placeholder="you@company.com">
      </div>
      <div class="form-group">
        <label class="form-label">Password</label>
        <input type="password" class="form-input" placeholder="••••••••">
      </div>
      <button type="submit" class="login-btn">Sign In</button>
    </form>
    
    <p class="login-footer">Don't have an account? <a href="#">Contact Admin</a></p>
  </div>
</body>
</html>
```

### Employee List Page

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Employees | AscendHR</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: system-ui, -apple-system, sans-serif; background: #F8FAFC; color: #334155; padding: 32px; }
    
    .page-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 24px; }
    .page-title { font-size: 24px; font-weight: 600; }
    .btn-primary { background: #3B82F6; color: white; border: none; padding: 10px 16px; font-size: 14px; font-weight: 500; border-radius: 8px; cursor: pointer; }
    
    .search-bar { display: flex; gap: 12px; margin-bottom: 24px; }
    .search-input { flex: 1; padding: 10px 12px; font-size: 14px; border: 1px solid #E2E8F0; border-radius: 8px; background: white; }
    .filter-btn { background: white; border: 1px solid #E2E8F0; padding: 10px 16px; font-size: 14px; border-radius: 8px; cursor: pointer; }
    
    .table-card { background: white; border: 1px solid #E2E8F0; border-radius: 12px; overflow: hidden; box-shadow: 0 2px 8px -2px rgba(51,65,85,0.08); }
    table { width: 100%; border-collapse: collapse; font-size: 14px; }
    th { text-align: left; padding: 14px 16px; font-weight: 500; color: #64748B; background: #F8FAFC; border-bottom: 1px solid #E2E8F0; }
    td { padding: 14px 16px; border-bottom: 1px solid #E2E8F0; }
    tr:last-child td { border-bottom: none; }
    tr:hover { background: #F8FAFC; }
    
    .avatar { width: 36px; height: 36px; background: #3B82F6; color: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 13px; font-weight: 600; }
    .employee-info { display: flex; align-items: center; gap: 12px; }
    .employee-name { font-weight: 500; }
    .employee-email { font-size: 13px; color: #64748B; }
    
    .badge { display: inline-flex; padding: 2px 10px; font-size: 12px; font-weight: 600; border-radius: 9999px; }
    .badge-active { background: #22C55E; color: white; }
    .badge-inactive { background: #F1F5F9; color: #64748B; }
    
    .actions { display: flex; gap: 8px; }
    .action-btn { background: none; border: none; color: #64748B; cursor: pointer; font-size: 14px; }
    .action-btn:hover { color: #3B82F6; }
  </style>
</head>
<body>
  <header class="page-header">
    <h1 class="page-title">Employees</h1>
    <button class="btn-primary">+ Add Employee</button>
  </header>

  <div class="search-bar">
    <input type="text" class="search-input" placeholder="Search employees...">
    <button class="filter-btn">🔽 Department</button>
    <button class="filter-btn">🔽 Status</button>
  </div>

  <div class="table-card">
    <table>
      <thead>
        <tr>
          <th>Employee</th>
          <th>Department</th>
          <th>Role</th>
          <th>Status</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>
            <div class="employee-info">
              <div class="avatar">JD</div>
              <div>
                <div class="employee-name">John Doe</div>
                <div class="employee-email">john@company.com</div>
              </div>
            </div>
          </td>
          <td>Engineering</td>
          <td>Senior Developer</td>
          <td><span class="badge badge-active">Active</span></td>
          <td class="actions">
            <button class="action-btn">✏️</button>
            <button class="action-btn">🗑️</button>
          </td>
        </tr>
        <tr>
          <td>
            <div class="employee-info">
              <div class="avatar">JS</div>
              <div>
                <div class="employee-name">Jane Smith</div>
                <div class="employee-email">jane@company.com</div>
              </div>
            </div>
          </td>
          <td>Design</td>
          <td>UI/UX Designer</td>
          <td><span class="badge badge-active">Active</span></td>
          <td class="actions">
            <button class="action-btn">✏️</button>
            <button class="action-btn">🗑️</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</body>
</html>
```

### Form Modal

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Modal Example</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: system-ui, -apple-system, sans-serif; background: #F8FAFC; color: #334155; }
    
    .modal-overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.5); display: flex; align-items: center; justify-content: center; }
    .modal { background: white; border-radius: 16px; width: 100%; max-width: 500px; box-shadow: 0 8px 32px -8px rgba(0,0,0,0.2); }
    .modal-header { padding: 20px 24px; border-bottom: 1px solid #E2E8F0; display: flex; justify-content: space-between; align-items: center; }
    .modal-title { font-size: 18px; font-weight: 600; }
    .modal-close { background: none; border: none; font-size: 20px; cursor: pointer; color: #64748B; }
    .modal-body { padding: 24px; }
    .modal-footer { padding: 16px 24px; border-top: 1px solid #E2E8F0; display: flex; justify-content: flex-end; gap: 12px; }
    
    .form-group { margin-bottom: 20px; }
    .form-label { display: block; font-size: 14px; font-weight: 500; margin-bottom: 6px; }
    .form-input { width: 100%; padding: 10px 12px; font-size: 14px; border: 1px solid #E2E8F0; border-radius: 8px; }
    
    .btn-secondary { background: #F1F5F9; color: #334155; border: none; padding: 10px 16px; font-size: 14px; font-weight: 500; border-radius: 8px; cursor: pointer; }
    .btn-primary { background: #3B82F6; color: white; border: none; padding: 10px 16px; font-size: 14px; font-weight: 500; border-radius: 8px; cursor: pointer; }
  </style>
</head>
<body>
  <div class="modal-overlay">
    <div class="modal">
      <div class="modal-header">
        <h2 class="modal-title">Add New Employee</h2>
        <button class="modal-close">×</button>
      </div>
      <div class="modal-body">
        <div class="form-group">
          <label class="form-label">Full Name</label>
          <input type="text" class="form-input" placeholder="Enter full name">
        </div>
        <div class="form-group">
          <label class="form-label">Email</label>
          <input type="email" class="form-input" placeholder="Enter email address">
        </div>
        <div class="form-group">
          <label class="form-label">Department</label>
          <select class="form-input">
            <option>Select department...</option>
            <option>Engineering</option>
            <option>Design</option>
            <option>Marketing</option>
            <option>HR</option>
          </select>
        </div>
        <div class="form-group">
          <label class="form-label">Role</label>
          <input type="text" class="form-input" placeholder="Enter role/position">
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn-secondary">Cancel</button>
        <button class="btn-primary">Save Employee</button>
      </div>
    </div>
  </div>
</body>
</html>
```

---

## 5. AI Agent Prompt

Use this system prompt when instructing AI agents to create mockups:

```
You are a UI/UX designer creating HTML mockups for AscendHR, a professional HRM system.

DESIGN SYSTEM RULES:
- Primary: #3B82F6 (blue)
- Success: #22C55E (green)
- Destructive: #EF4444 (red)
- Warning: #FACC15 (yellow)
- Background: #F8FAFC
- Card/White: #FFFFFF
- Text: #334155
- Text Muted: #64748B
- Border: #E2E8F0
- Gradient: linear-gradient(135deg, #3B82F6, #7C3AED)

TYPOGRAPHY:
- Font: system-ui, -apple-system, sans-serif
- Headings: 600-700 weight
- Sizes: 12px (xs), 14px (sm), 16px (base), 24px (xl), 30px (2xl)

SPACING:
- Border radius: 8px (buttons), 12px (cards), 9999px (badges)
- Shadows: 0 2px 8px -2px rgba(51,65,85,0.08)

OUTPUT: Generate complete HTML with inline CSS.
```

---

## 6. Available Components (50 shadcn/ui)

### Layout & Navigation
`Sidebar`, `NavigationMenu`, `Breadcrumb`, `Tabs`, `Accordion`, `Collapsible`

### Forms & Inputs
`Button`, `Input`, `Textarea`, `Select`, `Checkbox`, `RadioGroup`, `Switch`, `Slider`, `Form`, `Label`, `InputOTP`, `Calendar`

### Data Display
`Card`, `Table`, `Badge`, `Avatar`, `Progress`, `Skeleton`, `Chart`, `Carousel`

### Feedback
`Alert`, `AlertDialog`, `Dialog`, `Drawer`, `Sheet`, `Toast/Sonner`, `Tooltip`, `HoverCard`, `Popover`

### Menus
`DropdownMenu`, `ContextMenu`, `Menubar`, `Command`

### Utility
`ScrollArea`, `Separator`, `AspectRatio`, `Resizable`, `ToggleGroup`, `Toggle`, `Pagination`

---

## 7. Tech Stack

| Technology | Purpose |
|------------|---------|
| TailwindCSS 4.x | Utility-first CSS |
| shadcn/ui | Radix-based components |
| class-variance-authority | Variant management |
| tailwind-merge | Class conflict resolution |
| tailwindcss-animate | Animation utilities |
| next-themes | Theme switching |

---

## 8. 🎮 Gamification Mood & Tone (Football Manager / EA Sports FC Style)

> AscendHR adopts the visual language of Football Manager and EA Sports FC to make HR feel like managing a championship-winning squad.

### Design Philosophy

| Principle | Description |
|-----------|-------------|
| **Data is King** | Show stats prominently - employees are "players" with measurable abilities |
| **Visual Hierarchy** | Important numbers (ratings, scores) are large and bold |
| **Comparative** | Everything can be compared side-by-side |
| **Achievement-Driven** | Celebrate milestones, show progress |
| **Professional Gaming** | Serious but engaging, like managing a real team |

---

### 8.1 Player Card Component (FM-Style)

The signature component - every employee has a "Player Card" like Football Manager.

```html
<!-- FM-Style Player Card -->
<div style="
  width: 280px;
  background: linear-gradient(145deg, #FFFFFF 0%, #F8FAFC 100%);
  border: 1px solid #E2E8F0;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 4px 16px -4px rgba(51,65,85,0.12);
">
  <!-- Header with Photo -->
  <div style="
    background: linear-gradient(135deg, #3B82F6, #7C3AED);
    padding: 20px;
    text-align: center;
  ">
    <img src="https://i.pravatar.cc/80" style="
      width: 80px; height: 80px;
      border-radius: 50%;
      border: 3px solid white;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    ">
    <h3 style="color: white; margin: 12px 0 4px; font-size: 18px; font-weight: 600;">John Doe</h3>
    <p style="color: rgba(255,255,255,0.8); font-size: 13px;">Senior Developer</p>
  </div>
  
  <!-- Ability Rating -->
  <div style="
    display: flex;
    justify-content: space-around;
    padding: 16px;
    background: #F8FAFC;
    border-bottom: 1px solid #E2E8F0;
  ">
    <div style="text-align: center;">
      <div style="font-size: 28px; font-weight: 700; color: #22C55E;">85</div>
      <div style="font-size: 11px; color: #64748B; text-transform: uppercase;">Current</div>
    </div>
    <div style="text-align: center;">
      <div style="font-size: 28px; font-weight: 700; color: #3B82F6;">92</div>
      <div style="font-size: 11px; color: #64748B; text-transform: uppercase;">Potential</div>
    </div>
  </div>
  
  <!-- Attributes Preview -->
  <div style="padding: 16px;">
    <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
      <span style="font-size: 13px; color: #64748B;">Coding</span>
      <span style="font-size: 13px; font-weight: 600; color: #334155;">18</span>
    </div>
    <div style="background: #E2E8F0; border-radius: 4px; height: 6px; margin-bottom: 12px;">
      <div style="background: #22C55E; border-radius: 4px; height: 6px; width: 90%;"></div>
    </div>
    
    <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
      <span style="font-size: 13px; color: #64748B;">Leadership</span>
      <span style="font-size: 13px; font-weight: 600; color: #334155;">14</span>
    </div>
    <div style="background: #E2E8F0; border-radius: 4px; height: 6px;">
      <div style="background: #3B82F6; border-radius: 4px; height: 6px; width: 70%;"></div>
    </div>
  </div>
</div>
```

---

### 8.2 Attribute Bar Component (1-20 Scale)

Visual representation of skill levels like FM's attribute system.

```html
<!-- Single Attribute Bar -->
<div style="display: flex; align-items: center; gap: 12px; margin-bottom: 12px;">
  <span style="width: 100px; font-size: 13px; color: #64748B;">Coding</span>
  <div style="flex: 1; background: #E2E8F0; border-radius: 4px; height: 8px;">
    <div style="background: linear-gradient(90deg, #22C55E, #16A34A); border-radius: 4px; height: 8px; width: 90%;"></div>
  </div>
  <span style="width: 24px; font-size: 14px; font-weight: 600; color: #22C55E; text-align: right;">18</span>
</div>

<!-- Attribute with Color Coding -->
<!-- Green (15-20): Excellent -->
<!-- Blue (10-14): Good -->
<!-- Yellow (5-9): Average -->
<!-- Red (1-4): Weak -->
```

**Color Coding Rules:**
| Range | Color | Meaning |
|-------|-------|---------|
| 15-20 | `#22C55E` (Green) | Excellent / Star Quality |
| 10-14 | `#3B82F6` (Blue) | Good / Solid Performer |
| 5-9 | `#FACC15` (Yellow) | Average / Needs Development |
| 1-4 | `#EF4444` (Red) | Weak / Critical Gap |

---

### 8.3 Tier Badges (Player Rarity)

Like EA Sports FC card rarity system for employee classifications.

```html
<!-- Rookie Badge -->
<span style="
  display: inline-flex; align-items: center; gap: 6px;
  background: #A1A1AA; color: white;
  padding: 4px 12px; font-size: 12px; font-weight: 600;
  border-radius: 9999px;
">🔰 Rookie</span>

<!-- Standard Badge -->
<span style="
  display: inline-flex; align-items: center; gap: 6px;
  background: #3B82F6; color: white;
  padding: 4px 12px; font-size: 12px; font-weight: 600;
  border-radius: 9999px;
">⭐ Standard</span>

<!-- Gold Badge -->
<span style="
  display: inline-flex; align-items: center; gap: 6px;
  background: linear-gradient(135deg, #F59E0B, #D97706); color: white;
  padding: 4px 12px; font-size: 12px; font-weight: 600;
  border-radius: 9999px;
">🏆 Gold</span>

<!-- Elite Badge -->
<span style="
  display: inline-flex; align-items: center; gap: 6px;
  background: linear-gradient(135deg, #7C3AED, #5B21B6); color: white;
  padding: 4px 12px; font-size: 12px; font-weight: 600;
  border-radius: 9999px;
">💎 Elite</span>

<!-- Legend Badge -->
<span style="
  display: inline-flex; align-items: center; gap: 6px;
  background: linear-gradient(135deg, #1E293B, #0F172A); color: #F59E0B;
  padding: 4px 12px; font-size: 12px; font-weight: 600;
  border-radius: 9999px;
  border: 1px solid #F59E0B;
">👑 Legend</span>
```

**Tier System:**
| Tier | When to Use | Visual Style |
|------|-------------|--------------|
| Rookie | New employees (< 6 months) | Gray, minimal |
| Standard | Regular employees | Blue, solid |
| Gold | High performers | Gold gradient |
| Elite | Top talent / Key players | Purple gradient |
| Legend | Executives / Company icons | Black with gold |

---

### 8.4 XP & Progress Bars (Onboarding/Training)

Gamification of progress like leveling up.

```html
<!-- XP Progress Bar -->
<div style="margin-bottom: 16px;">
  <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
    <span style="font-size: 14px; font-weight: 500; color: #334155;">Onboarding Progress</span>
    <span style="font-size: 14px; font-weight: 600; color: #3B82F6;">Level 3</span>
  </div>
  <div style="background: #E2E8F0; border-radius: 9999px; height: 12px; overflow: hidden;">
    <div style="
      background: linear-gradient(90deg, #3B82F6, #7C3AED);
      height: 12px;
      width: 65%;
      transition: width 0.5s ease;
    "></div>
  </div>
  <div style="display: flex; justify-content: space-between; margin-top: 4px;">
    <span style="font-size: 12px; color: #64748B;">650 / 1000 XP</span>
    <span style="font-size: 12px; color: #64748B;">35% to Level 4</span>
  </div>
</div>

<!-- Milestone Indicators -->
<div style="display: flex; justify-content: space-between; padding: 0 8px;">
  <div style="text-align: center;">
    <div style="width: 24px; height: 24px; background: #22C55E; border-radius: 50%; margin: 0 auto 4px; display: flex; align-items: center; justify-content: center; color: white; font-size: 12px;">✓</div>
    <span style="font-size: 10px; color: #64748B;">Profile</span>
  </div>
  <div style="text-align: center;">
    <div style="width: 24px; height: 24px; background: #22C55E; border-radius: 50%; margin: 0 auto 4px; display: flex; align-items: center; justify-content: center; color: white; font-size: 12px;">✓</div>
    <span style="font-size: 10px; color: #64748B;">Training</span>
  </div>
  <div style="text-align: center;">
    <div style="width: 24px; height: 24px; background: #3B82F6; border-radius: 50%; margin: 0 auto 4px; display: flex; align-items: center; justify-content: center; color: white; font-size: 12px;">3</div>
    <span style="font-size: 10px; color: #3B82F6; font-weight: 500;">Tasks</span>
  </div>
  <div style="text-align: center;">
    <div style="width: 24px; height: 24px; background: #E2E8F0; border-radius: 50%; margin: 0 auto 4px; display: flex; align-items: center; justify-content: center; color: #64748B; font-size: 12px;">4</div>
    <span style="font-size: 10px; color: #64748B;">Review</span>
  </div>
</div>
```

---

### 8.5 Stat Comparison Layout (Side-by-Side)

Compare players/employees like FM's comparison screen.

```html
<!-- Stat Comparison -->
<div style="display: flex; gap: 16px;">
  <!-- Player 1 -->
  <div style="flex: 1; background: white; border: 1px solid #E2E8F0; border-radius: 12px; padding: 20px;">
    <div style="text-align: center; margin-bottom: 16px;">
      <div style="width: 60px; height: 60px; background: #3B82F6; color: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 20px; font-weight: 600; margin: 0 auto 8px;">JD</div>
      <div style="font-weight: 600;">John Doe</div>
      <div style="font-size: 13px; color: #64748B;">Developer</div>
    </div>
    <div style="font-size: 13px;">
      <div style="display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px solid #E2E8F0;">
        <span style="color: #64748B;">Coding</span>
        <span style="font-weight: 600; color: #22C55E;">18</span>
      </div>
      <div style="display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px solid #E2E8F0;">
        <span style="color: #64748B;">Leadership</span>
        <span style="font-weight: 600; color: #3B82F6;">12</span>
      </div>
      <div style="display: flex; justify-content: space-between; padding: 8px 0;">
        <span style="color: #64748B;">Teamwork</span>
        <span style="font-weight: 600; color: #22C55E;">16</span>
      </div>
    </div>
  </div>
  
  <!-- VS Divider -->
  <div style="display: flex; align-items: center;">
    <div style="background: #3B82F6; color: white; padding: 8px 12px; border-radius: 8px; font-weight: 600; font-size: 14px;">VS</div>
  </div>
  
  <!-- Player 2 -->
  <div style="flex: 1; background: white; border: 1px solid #E2E8F0; border-radius: 12px; padding: 20px;">
    <!-- Similar structure -->
  </div>
</div>
```

---

### 8.6 Achievement Badges

Celebrate milestones with game-like achievements.

```html
<!-- Achievement Unlocked -->
<div style="
  display: flex; align-items: center; gap: 16px;
  background: linear-gradient(135deg, #F0FDF4, #DCFCE7);
  border: 1px solid #22C55E;
  border-radius: 12px;
  padding: 16px;
">
  <div style="
    width: 48px; height: 48px;
    background: linear-gradient(135deg, #22C55E, #16A34A);
    border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    font-size: 24px;
  ">🏆</div>
  <div>
    <div style="font-size: 12px; color: #22C55E; font-weight: 600; text-transform: uppercase;">Achievement Unlocked</div>
    <div style="font-size: 16px; font-weight: 600; color: #334155;">First Squad Complete</div>
    <div style="font-size: 13px; color: #64748B;">Added 10 players to your squad</div>
  </div>
</div>

<!-- Achievement Badge (Small) -->
<div style="
  display: inline-flex; align-items: center; gap: 8px;
  background: #F8FAFC;
  border: 1px solid #E2E8F0;
  border-radius: 8px;
  padding: 8px 12px;
">
  <span style="font-size: 20px;">🎯</span>
  <div>
    <div style="font-size: 12px; font-weight: 600; color: #334155;">Goal Setter</div>
    <div style="font-size: 11px; color: #64748B;">Set 5 team goals</div>
  </div>
</div>
```

---

### 8.7 Formation Diagram (Org Chart as Pitch)

Visual team layout like FM's formation view.

```html
<!-- Formation Preview (Mini) -->
<div style="
  background: linear-gradient(180deg, #22C55E 0%, #16A34A 100%);
  border-radius: 12px;
  padding: 20px;
  position: relative;
  min-height: 200px;
">
  <!-- Pitch Lines -->
  <div style="
    position: absolute;
    top: 50%;
    left: 10%;
    right: 10%;
    height: 1px;
    background: rgba(255,255,255,0.3);
  "></div>
  <div style="
    position: absolute;
    top: 10%;
    left: 50%;
    transform: translateX(-50%);
    width: 60px;
    height: 60px;
    border: 1px solid rgba(255,255,255,0.3);
    border-radius: 50%;
  "></div>
  
  <!-- Player Positions -->
  <div style="
    position: absolute;
    top: 75%;
    left: 50%;
    transform: translateX(-50%);
    text-align: center;
  ">
    <div style="width: 36px; height: 36px; background: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 12px; font-weight: 600; box-shadow: 0 2px 8px rgba(0,0,0,0.2);">CEO</div>
  </div>
  
  <!-- Add more positions... -->
</div>
```

---

### 8.8 Gamification Language

Use football/gaming terminology consistently.

| HR Term | Gamified Term | Usage |
|---------|---------------|-------|
| Employee | Player | "Add a new player to your squad" |
| Employees | Squad | "Your squad has 45 players" |
| Manager | Coach / Manager | "Assign a coach to this team" |
| Department | Team | "Engineering Team" |
| Company | Club | "Manchester Tech FC" |
| Skills | Attributes | "Rate player attributes 1-20" |
| Performance | Ability Rating | "Current Ability: 85" |
| Potential | Potential Rating | "Potential Ability: 92" |
| Onboarding | Training Camp | "Complete training camp" |
| Org Chart | Formation View | "View squad formation" |
| Promotion | Transfer / Level Up | "Level up to Senior" |
| Termination | Released | "Player released from squad" |
| Recruiting | Scouting | "Scout new talent" |
| Candidates | Scouted Players | "5 players in scouting pipeline" |
| KPIs | Stats | "Player stats this quarter" |
| Goals | Objectives | "Team objectives this season" |

---

### 8.9 Radar Chart Guidelines (CSS/Canvas)

For visualizing multiple attributes at once.

```html
<!-- Radar Chart Container -->
<div style="
  width: 200px;
  height: 200px;
  background: white;
  border-radius: 12px;
  border: 1px solid #E2E8F0;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
">
  <!-- Use Chart.js or similar for actual radar chart -->
  <!-- This is a placeholder structure -->
  <canvas id="radarChart" width="180" height="180"></canvas>
</div>

<!-- Radar Chart Script (Chart.js) -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
const ctx = document.getElementById('radarChart').getContext('2d');
new Chart(ctx, {
  type: 'radar',
  data: {
    labels: ['Coding', 'Design', 'Leadership', 'Teamwork', 'Creativity', 'Analysis'],
    datasets: [{
      data: [18, 12, 14, 16, 15, 17],
      backgroundColor: 'rgba(59, 130, 246, 0.2)',
      borderColor: '#3B82F6',
      borderWidth: 2,
      pointBackgroundColor: '#3B82F6'
    }]
  },
  options: {
    scales: {
      r: {
        beginAtZero: true,
        max: 20,
        ticks: { stepSize: 5 }
      }
    },
    plugins: { legend: { display: false } }
  }
});
</script>
```

**Radar Chart Color Mapping:**
- Current Ability: Blue (`#3B82F6`)
- Potential Ability: Purple (`#7C3AED`)
- Comparison Player: Gray (`#94A3B8`)
