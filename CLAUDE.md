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
│   └── BaseLayout.astro    # Base HTML layout with Header, Footer, scroll animations
├── pages/
│   ├── index.astro         # Landing page
│   ├── privacy.astro       # Privacy policy
│   ├── support.astro       # Support & FAQ
│   └── components.astro    # Component showcase (temporary, for visual testing)
├── components/
│   ├── Button.astro        # Primary/secondary variants, neumorphic, href/button
│   ├── Card.astro          # Neumorphic raised card, configurable padding
│   ├── SectionHeading.astro # Peddana title + optional handwritten annotation
│   ├── Icon.astro          # SVG icons: shield, check, moon, palette
│   ├── AppStoreBadge.astro # Apple/Google store badges
│   ├── Header.astro       # Sticky header with branding + nav (showAnchors prop)
│   ├── Footer.astro       # Tagline, links, copyright
│   ├── Hero.astro         # Landing page hero with branding, tagline, badges
│   ├── FeatureCard.astro  # Neumorphic card with icon, title, description
│   ├── FeaturesSection.astro # 4-card feature grid (privacy, simplicity, calm, themes)
│   ├── PhoneMockup.astro  # CSS phone frame with slot for screenshot content
│   ├── PreviewSection.astro # Phone mockup with app preview and caption
│   └── ThemesSection.astro # Color palette swatches for 4 themes
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
- `.neu-flat` — Flat with subtle border
- `.neu-button` — Interactive button with hover states

### Components

| Component | Props | Description |
|-----------|-------|-------------|
| `Button` | `variant`, `href`, `size` | Primary (dark bg) / secondary (light bg), renders as `<a>` or `<button>` |
| `Card` | `padding`, `class` | Neumorphic raised card with sm/md/lg padding |
| `SectionHeading` | `title`, `annotation`, `align` | Section title in Peddana + optional handwritten note |
| `Icon` | `name`, `size`, `class` | SVG icons: shield, check, moon, palette |
| `AppStoreBadge` | `store`, `href` | Apple App Store / Google Play badge |
| `Header` | `showAnchors` | Sticky header, branding + nav. Anchors hidden on subpages |
| `Footer` | — | Tagline, privacy/support links, copyright |
| `Hero` | — | Landing page hero: branding, tagline, anti-feature callout, badges |
| `FeatureCard` | `icon`, `title`, `description` | Neumorphic card with icon, Peddana title, description |
| `FeaturesSection` | — | 4 feature cards in responsive grid |
| `PhoneMockup` | `class` | CSS phone frame with notch, slot for screen content |
| `PreviewSection` | — | Phone mockup with placeholder app UI and caption |
| `ThemesSection` | — | Color palette swatches (4 themes) with freemium note |

## Session Progress

- [x] Session 1: Project scaffolding & configuration
- [x] Session 2: Design system & core components
- [x] Session 3: Landing page structure
- [x] Session 4: Landing page content sections
- [ ] Session 5: Privacy policy page
- [ ] Session 6: Support page & final polish
- [ ] Session 7: Deployment & launch
