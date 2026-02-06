# Small Talk Website

Landing page, privacy policy, and support page for Small Talk Notebook app.

## Quick Start

```bash
npm install
npm run dev     # Start dev server at localhost:4321
npm run build   # Build to dist/
```

## Key Documents

- `IMPLEMENTATION_PLAN.md` — Full website spec: sessions, design system, content, deployment

## Project Structure

```
src/
├── layouts/
│   └── BaseLayout.astro    # Base HTML layout with meta tags
├── pages/
│   ├── index.astro         # Landing page
│   ├── privacy.astro       # Privacy policy
│   └── support.astro       # Support & FAQ
├── components/             # Reusable Astro components (Session 2+)
└── styles/
    └── global.css          # Tailwind + theme variables + neumorphic utilities
public/
└── fonts/                  # Self-hosted font files
```

## Design System

### Color Palette (Morning Window)

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
- `.neu-button` — Interactive button with hover states

## Session Progress

- [x] Session 1: Project scaffolding & configuration
- [ ] Session 2: Design system & core components
- [ ] Session 3: Landing page structure
- [ ] Session 4: Landing page content sections
- [ ] Session 5: Privacy policy page
- [ ] Session 6: Support page & final polish
- [ ] Session 7: Deployment & launch
