# Small Talk Notebook — Implementation Plan

> All sessions complete. Website is deployed to GitHub Pages with custom domain.

---

## Session Progress

- [x] Session 1: Project scaffolding & configuration
- [x] Session 2: Design system & core components
- [x] Session 3: Landing page structure
- [x] Session 4: Landing page content sections
- [x] Session 5: Privacy policy page
- [x] Session 6: Support page & FAQ
- [x] Session 7: Deployment & launch

---

## Session 7: Deployment & Launch — Completed

### Done

- [x] Configured Astro for GitHub Pages (`site`, `output: 'static'` in astro.config.mjs)
- [x] Added `CNAME` file for custom domain (`smalltalknotebook.com`)
- [x] Created GitHub Actions workflow (`.github/workflows/deploy.yml`) — auto-deploys on push to master
- [x] Added SEO meta tags: canonical URL, `og:url`, `og:image`, `twitter:image`
- [x] Removed `components.astro` (temporary showcase page)
- [x] Removed `privacy_policy_plan.md` (reference doc)
- [x] Favicon, apple-touch-icon, and site.webmanifest already in place from earlier sessions
- [x] No link prefixing needed (custom domain uses `base: '/'`)

### Remaining (manual steps)

- [ ] **Purchase domain** (`smalltalknotebook.com`) from a registrar
- [ ] **Configure DNS** — point to GitHub Pages:
  - A records: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
  - CNAME record: `www` → `Kieran-LaMee.github.io`
- [ ] **Enable GitHub Pages** in repo Settings → Pages → Source: GitHub Actions
- [ ] **Set custom domain** in repo Settings → Pages → Custom domain: `smalltalknotebook.com`
- [ ] **Verify support email** — confirm `support@smalltalknotebook.com` is configured and receiving mail
- [ ] **App Store URLs** — update `href="#"` placeholders in Hero.astro once apps are listed

### Optional / Future

- [ ] Create dedicated OG image (1200x630) for better social sharing previews (currently uses app icon)
- [ ] Privacy policy legal refinements (entity name, jurisdiction, mailing address)
- [ ] Lighthouse audit (target: Performance >90, Accessibility 100, SEO >90)

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
