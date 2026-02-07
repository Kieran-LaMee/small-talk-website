# Small Talk Notebook — Remaining Implementation Tasks

> Everything below is what's left. Sessions 1–6 are complete (scaffolding, design system, components, landing page, privacy policy, support page).

---

## Assets Needed

These are blockers for a production-ready launch.

### Required

- [ ] **App icon** (PNG, 512x512 minimum) — needed for favicon, apple-touch-icon, OG image
- [ ] **App Store URL** — or decide on "Coming Soon" strategy (currently `href="#"` in Hero.astro)
- [ ] **Play Store URL** — same as above
- [ ] **Verify support email** — `support@smalltalknotebook.com` is used in privacy.astro and support.astro; confirm it's configured and receiving mail

### Recommended

- [ ] **App screenshots** (2-3 real screenshots for phone mockup) — currently using CSS placeholder UI in PreviewSection.astro
- [ ] **OG image** (1200x630) — for social sharing previews. Currently no `og:image` content is set.

---

## Privacy Policy — Legal Decisions

The privacy policy content is implemented in `privacy.astro`. The `privacy_policy_plan.md` file documents Termly questionnaire answers. Before publishing, you need to decide:

- [ ] **Legal name or business entity** — for "who operates this app" (currently just says "Small Talk Notebook")
- [ ] **Country / state** — determines which laws apply (GDPR, CCPA, etc.)
- [ ] **Physical mailing address** — GDPR may require it
- [ ] **"Do Not Track" statement** — standard in US-facing policies
- [ ] **Governing law / jurisdiction** — which country/state's laws govern

Once decided, either update `privacy.astro` directly or generate a formal policy through Termly and replace the current content.

---

## Pre-Launch Polish

### SEO & Meta

- [ ] Add `og:image` meta tag to BaseLayout.astro (needs OG image asset first)
- [ ] Add canonical URLs (`<link rel="canonical">`) to BaseLayout.astro
- [ ] Add `og:url` meta tag to BaseLayout.astro

### Favicon & Icons

- [ ] Replace default `favicon.svg` / `favicon.ico` with app icon
- [ ] Add `apple-touch-icon.png` (180x180) to `public/`
- [ ] Add `site.webmanifest` to `public/`
- [ ] Update `<link>` tags in BaseLayout.astro head

### Cleanup

- [ ] Remove `components.astro` page (temporary showcase, not for production)
- [ ] Remove `privacy_policy_plan.md` (reference doc, not needed in deployed site — or add to `.gitignore`)

### Testing (Optional but Recommended)

- [ ] Run Lighthouse audit (target: Performance >90, Accessibility 100, SEO >90)
- [ ] Test on mobile (iOS Safari, Android Chrome)
- [ ] Verify all links work including anchor scrolls

---

## Deployment (Session 7)

### Configure Astro for GitHub Pages

Update `astro.config.mjs`:

```javascript
export default defineConfig({
  site: 'https://kieran-lamee.github.io',
  base: '/small-talk-website',
  output: 'static',
  // ...existing vite config
});
```

**Important:** Setting `base` means all internal links (`/privacy`, `/support`, `/`, `/#features`, etc.) must be prefixed with the base path. Every `href` in Header.astro, Footer.astro, privacy.astro, support.astro, and components.astro (if kept) needs updating to use `import.meta.env.BASE_URL`.

If using a custom domain instead, set `base: '/'` and skip link prefixing.

### GitHub Actions Workflow

Create `.github/workflows/deploy.yml` using Astro's official GitHub Pages deployment action. Trigger on push to `master`.

### Internal Link Updates for Base Path

Files with absolute links that need prefixing:

| File | Links |
|------|-------|
| `Header.astro` | `/` (brand), `/#features`, `/#preview`, `/#themes`, `/privacy`, `/support` |
| `Footer.astro` | `/privacy`, `/support` |
| `privacy.astro` | `/` (back link) |
| `support.astro` | `/` (back link) |
| `BaseLayout.astro` | `/favicon.svg` |

### Post-Deploy Verification

- [ ] All pages load at public URL
- [ ] HTTPS working
- [ ] OG image appears in social previews (test with opengraph.xyz or similar)
- [ ] App store badge links work (or are clearly placeholder)
- [ ] Deployment triggers automatically on push

### Optional

- [ ] Configure custom domain (add CNAME to `public/`, configure DNS)
- [ ] Set up redirects (`/privacy-policy` → `/privacy`)
- [ ] Update repo README with actual project info (currently has Astro starter template boilerplate)

---

## Reference

### Brand Guidelines Quick Reference

**Voice:** Calm, minimal. Short sentences. Fragments OK. Speak like a thoughtful friend.

**Words to avoid:** optimize, hack, leverage, 10x, solutions, empower, revolutionary, game-changing

**Key messages:**
1. Simplicity is the feature
2. Privacy by design — no accounts, no cloud, no tracking
3. No demands — no streaks, no notifications, no guilt
4. Generous free — pay once for extras

**Freemium copy standard:** "Everything you need is free. Unlock extra themes and export with a one-time purchase."

### Design System

Fully documented in `CLAUDE.md` — color palette, fonts, neumorphic classes, component props.
