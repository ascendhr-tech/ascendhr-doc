# AscendHR Shared Components

This folder contains centralized CSS and layout components for all HTML mockups.

## Usage

Include in any HTML mockup:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title | AscendHR</title>
  <!-- SHARED COMPONENT SYSTEM -->
  <link rel="stylesheet" href="../_shared/base.css">
</head>
<body>
  <!-- Your content here -->
</body>
</html>
```

## Files

| File | Purpose |
|------|---------|
| `base.css` | Complete design system: tokens, components, layouts |

## Available Components

### Buttons
- `.btn` - Base button
- `.btn-primary` - Primary action (blue)
- `.btn-secondary` - Secondary action (gray)
- `.btn-destructive` - Destructive action (red)
- `.btn-outline` - Outline style
- `.btn-gradient` - Gradient hero button
- `.btn-lg`, `.btn-sm` - Size variants

### Cards
- `.card` - Base card with border and shadow
- `.card-hover` - Card with hover effect
- `.card-title`, `.card-description` - Card content

### Badges
- `.badge` - Base badge
- `.badge-primary`, `.badge-success`, `.badge-warning`, `.badge-destructive`
- `.badge-attack`, `.badge-midfield`, `.badge-defense`, `.badge-support` (Zone colors)

### Forms
- `.form-group` - Form field container
- `.form-label` - Input label
- `.form-input`, `.form-select`, `.form-textarea` - Input fields
- `.form-hint`, `.form-error` - Helper texts
- `.form-row` - Two-column layout

### Tables
- `.table-card` - Table container with styling
- Standard `table`, `th`, `td` styles included

### Avatars
- `.avatar` - Base avatar (circular)
- `.avatar-sm`, `.avatar-md`, `.avatar-lg`, `.avatar-xl` - Size variants

### Alerts
- `.alert` - Base alert
- `.alert-info`, `.alert-success`, `.alert-warning`, `.alert-error`

### Layouts
- `.app-container` - Main app wrapper (flex)
- `.sidebar` - Fixed left sidebar
- `.main-content` - Right content area
- `.wizard-container`, `.wizard-sidebar`, `.wizard-main` - Onboarding wizard
- `.modal-overlay`, `.modal`, `.modal-header`, `.modal-body`, `.modal-footer`
- `.page-header`, `.page-title` - Page top section

### Gamification Components
- `.pitch-container` - Green football pitch background
- `.pitch-node` - Position marker on pitch
- `.player-card-mini` - Small player card with fit score
- `.fit-score.high`, `.fit-score.medium`, `.fit-score.low` - Score colors

### Grid
- `.grid-2`, `.grid-3`, `.grid-4` - Column grids

### Utilities
- `.text-center`, `.text-muted`, `.text-primary`, etc.
- `.mb-2`, `.mb-4`, `.mb-6`, `.mb-8`, `.mt-4`, `.mt-6`
- `.flex`, `.flex-col`, `.items-center`, `.justify-between`
