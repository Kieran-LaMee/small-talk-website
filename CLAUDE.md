# Small Talk Website

Landing page, privacy policy, and support page for Small Talk Notebook app.

## Quick Start

```bash
npm install
npm run dev     # Start dev server at localhost:4321
npm run build   # Build to dist/
```

## Design System

### Color Palette (Morning Light)

```css
--color-bg-primary: #FFF8F0;    /* Pale cream */
--color-bg-secondary: #A1A69F;  /* Sage green */
--color-contrast: #2E4A3A;      /* Deep green */
--color-highlight: #8B4926;     /* Terracotta */
--color-muted: #7A6B5A;         /* Taupe */
```

### Fonts

| Role | Font | Class |
|------|------|-------|
| Body | Lato | `.font-body` (default) |
| Titles | Peddana | `.font-title` |
| Handwritten | Caveat | `.font-handwritten` |

### Neumorphic Classes

- `.neu-raised` — Raised card style
- `.neu-raised-sm` — Subtle raised style
- `.neu-pressed` — Inset/pressed style
- `.neu-flat` — Flat with subtle border
- `.neu-button` — Interactive button with hover states

Components are Astro files in `src/components/` — read individual files for props and usage.