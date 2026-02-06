# Small Talk Notebook — Website Implementation Plan

> A calm, minimal website that lets the design speak. Sparse words. Generous space. Trust and relief.

---

## 1. Overview

### Purpose

The website serves three functions:

1. **App Landing Page** — Introduce Small Talk Notebook to potential users
2. **Privacy Policy** — Required for App Store and Play Store submissions
3. **Support** — Provide a way for users to get help or report issues

### Target Audience

- **Forgetful introverts** — People who care deeply about others but struggle to remember details
- **Social connectors** — People who maintain many relationships and want to be more thoughtful

These users are tired of noisy apps, bloated tools, and systems that demand their attention. They want something that works quietly in the background of their lives.

### Brand Voice

**Calm & minimal.** Let the design do the talking. When we do use words:

- Short sentences. Sometimes fragments.
- No productivity language ("optimize," "hack," "leverage," "10x")
- No corporate speak ("solutions," "empower," "synergy")
- No hype ("revolutionary," "game-changing," "amazing")
- Speak like a thoughtful friend, not a marketing team

**Desired feelings when visiting the site:**
- **Trust** — "This feels safe and well-made."
- **Relief** — "Finally, something simple that respects me."

### Design Philosophy

The website should feel like a natural extension of the app:

- **Neumorphic visual style** — Soft shadows, raised components, no harsh edges
- **Same typography** — Lato (body), Peddana (titles), handwritten accent font
- **Same color palettes** — Morning Window as default, others as accents or demos
- **Calm, unhurried animations** — 400-500ms, ease-in-out, never jarring
- **Generous whitespace** — Breathable layouts that don't overwhelm
- **Paper-like texture** — Subtle grain or plaster-like background

### What It Is Not

- Not a flashy marketing site with aggressive CTAs
- Not a complex web app with dynamic features
- Not cluttered with social proof, testimonials, or urgency tactics
- Not trying to impress with features — simplicity is the feature

### Positioning

Small Talk is the antidote to:

| Category | What they do | What we do instead |
|----------|--------------|-------------------|
| **CRMs** (HubSpot, Salesforce) | Cold, transactional, business-focused | Warm, personal, relationship-focused |
| **Social media** | Noisy, performative, notification-heavy | Quiet, private, zero notifications |
| **Note apps** (Notion, Evernote) | Overwhelming, feature-bloated, requires setup | One thing, done well, works immediately |

The website should feel like opening a well-designed notebook — quiet, intentional, inviting.

---

## 2. Technical Stack

### Framework: Astro

**Why Astro:**
- Static-first, perfect for a simple landing page
- Zero JavaScript by default (fast, accessible)
- Component-based architecture
- Easy deployment to GitHub Pages, Netlify, or Vercel
- Excellent developer experience

### Styling: TailwindCSS + Custom CSS

**TailwindCSS** for utility classes and rapid development.

**Custom CSS** for:
- Neumorphic shadow utilities (not built into Tailwind)
- Paper texture backgrounds
- Font-face declarations for custom fonts

### Fonts

| Role | Font | Source | License |
|------|------|--------|---------|
| Body | Lato | Self-hosted | SIL OFL |
| Titles | Peddana | Self-hosted | SIL OFL |
| Handwritten | Caveat | Self-hosted | SIL OFL |

**Why self-host:**
- **Privacy alignment** — Google Fonts allows Google to track visitors. For a privacy-focused app, this creates messaging dissonance.
- **Performance** — Eliminates external DNS lookup and connection. Fonts load from same CDN as site.
- **Reliability** — No dependency on third-party service availability.
- **GDPR compliance** — Avoids potential issues in EU (Google Fonts has faced legal challenges).

**Setup:** Download font files from Google Fonts, convert to WOFF2 format, serve from `public/fonts/`.

Note: The app uses Pecita for handwritten text, but Caveat is a suitable web alternative. If Pecita licensing (check the license file in the app assets) permits web use, we can self-host Pecita instead for consistency.

### Deployment

**Primary:** GitHub Pages (free, simple, works with public repo)

**Alternative:** Netlify or Vercel (if more features needed)

The website will live in a separate public repository: `small-talk-website`

---

## 3. Design System

### Color Palettes

The website will use the same palette system as the app. Morning Window is the default.

#### Morning Window (Default)

```css
--color-bg-primary: #FFF8F0;      /* Pale cream */
--color-bg-secondary: #A1A69F;    /* Sage green */
--color-contrast: #2E4A3A;        /* Deep green */
--color-white: #FFFFFF;
--color-black: #1E1E1E;
--color-highlight: #8B4926;       /* Terracotta */
--color-muted: #7A6B5A;           /* Taupe */
```

#### Additional Palettes (for theme preview section)

Late Afternoon, Evening At Home, Nautical, Potted Fern, Grayscale, High Contrast, Arcade — all defined in the app's `color_palette.dart`.

### Neumorphic Styles

Neumorphism creates depth through dual shadows (dark below/right, light above/left).

**Raised (convex) elements** — Cards, buttons:
```css
.neu-raised {
  background: var(--color-bg-primary);
  border-radius: 16px;
  box-shadow:
    6px 6px 12px rgba(0, 0, 0, 0.1),
    -6px -6px 12px rgba(255, 255, 255, 0.7);
}
```

**Pressed (concave) elements** — Inputs, active states:
```css
.neu-pressed {
  background: var(--color-bg-primary);
  border-radius: 16px;
  box-shadow:
    inset 4px 4px 8px rgba(0, 0, 0, 0.1),
    inset -4px -4px 8px rgba(255, 255, 255, 0.7);
}
```

**Flat with border** — Subtle containers:
```css
.neu-flat {
  background: var(--color-bg-primary);
  border: 1px solid rgba(0, 0, 0, 0.05);
  border-radius: 16px;
}
```

### Typography Scale

```css
/* Titles - Peddana */
.title-xl { font-family: 'Peddana'; font-size: 4rem; line-height: 1.1; }
.title-lg { font-family: 'Peddana'; font-size: 2.5rem; line-height: 1.2; }
.title-md { font-family: 'Peddana'; font-size: 1.75rem; line-height: 1.3; }

/* Body - Lato */
.body-lg { font-family: 'Lato'; font-size: 1.25rem; line-height: 1.6; }
.body-md { font-family: 'Lato'; font-size: 1rem; line-height: 1.6; }
.body-sm { font-family: 'Lato'; font-size: 0.875rem; line-height: 1.5; }

/* Handwritten - Caveat */
.handwritten { font-family: 'Caveat'; font-size: 1.5rem; }
```

### Animation Principles

- **Duration:** 400-500ms for major transitions, 200-300ms for micro-interactions
- **Easing:** `ease-in-out` or `cubic-bezier(0.4, 0, 0.2, 1)`
- **Scroll animations:** Subtle fade-in and slide-up on scroll (IntersectionObserver)
- **Hover states:** Gentle shadow expansion, slight lift

### Spacing System

Use Tailwind's default spacing scale with generous application:
- Section padding: `py-16` to `py-24` (4rem to 6rem)
- Component gaps: `gap-6` to `gap-8` (1.5rem to 2rem)
- Card padding: `p-6` to `p-8` (1.5rem to 2rem)

---

## 4. Site Structure

### Pages

```
/                   → Landing page (index)
/privacy            → Privacy policy
/support            → Support & contact
```

### Landing Page Sections

1. **Hero** — Branding, tagline, app store buttons
2. **Features** — 3-4 key benefits with icons
3. **Preview** — Phone mockups showing the app
4. **Themes** — Color palette showcase (optional)
5. **Footer** — Links to privacy, support, copyright

### Navigation

Minimal navigation — just anchor links in the hero or a simple sticky header:
- Features (anchor)
- Preview (anchor)
- Privacy (link)
- Support (link)

No hamburger menu needed for this scope.

---

## 5. Content Requirements

### Copy

#### Hero Section

| Element | Primary Option | Alternates |
|---------|---------------|------------|
| **Tagline** | "A quiet place for the people you know." | "Remember the details. Forget the complexity." / "Less app. More notebook." |
| **Subtitle** | "Just names, notes, and nothing else." | "The details that matter. Nothing that doesn't." |

#### Features Section

Use a "what it doesn't do" framing to emphasize simplicity:

| Feature | Title | Description |
|---------|-------|-------------|
| **Privacy** | Truly private | Nothing leaves your phone. No accounts. No cloud. No sync. |
| **Simplicity** | Just one thing | Add people. Write notes. That's it. No features to learn. |
| **Calm** | No demands | No streaks. No reminders. No notifications. No guilt. |
| **Personal** | Make it yours | Choose a palette that feels like you. (Paid feature) |

#### Anti-Feature Callout (optional hero element)

A small, understated list that signals what kind of app this is:

```
No accounts. No cloud. No sync.
No streaks. No reminders. No guilt.
Just names, notes, and quiet.
```

#### Footer

| Element | Content |
|---------|---------|
| **Tagline** | "For the details that matter." |
| **Alternate** | "Less is more. That's it. That's the app." |

#### Freemium Messaging

Avoid "free tier" language. Frame it as generous defaults with optional extras:

- **On landing page:** "Everything you need is free. Unlock more themes and export with a one-time purchase."
- **On pricing (if shown):** "Free forever. Pay once if you want more."
- **Avoid:** "Free version," "premium," "upgrade," "tier"

### Assets Needed

| Asset | Description | Source |
|-------|-------------|--------|
| App icon | PNG, multiple sizes | Export from Flutter assets |
| Screenshots | 3-5 app screens | Capture from simulator/device |
| Phone mockup | Device frame for screenshots | Free mockup resource or CSS |
| App Store badge | Download on App Store | Apple Marketing Resources |
| Play Store badge | Get it on Google Play | Google Play Badge Generator |

### Privacy Policy Content

The privacy policy should cover:

1. **What data is collected** — None transmitted; all stored locally
2. **How data is stored** — On your device, encrypted (avoid jargon like "SQLCipher" — say "encrypted" or "bank-level encryption")
3. **Third-party services** — None. No analytics, no cloud, no tracking.
4. **Data sharing** — Never. Your notes never leave your device.
5. **User rights** — Full control. Delete everything anytime.
6. **Contact** — Email for privacy questions

**Tone guidance:** Write like a human, not a lawyer. Short sentences. Plain language. The privacy policy itself should feel like relief.

Example opening:
> "Small Talk Notebook is private by design. Your notes never leave your device. We don't have accounts, so we don't know who you are. We don't have servers, so we can't see your data. There's nothing to hack because there's nothing to steal."

### Support Page Content

- **FAQ section** — Common questions (see Session 6 for full list)
- **Contact** — Email address for support
- **Bug reports** — Link to GitHub Issues (if public) or email

### FAQ Content (Reframed Positively)

Frame questions to lead with value, not limitations:

| Question | Answer |
|----------|--------|
| **Where is my data stored?** | On your device. Only your device. No cloud, no sync, no accounts, no third parties. Your notebook, your business. |
| **Can I take my notes with me?** | Export is coming soon. For now, your data lives safely on your phone. |
| **How much does it cost?** | Everything you need is free. Pay once to unlock extra themes and export — no subscriptions, no recurring charges. |
| **What platforms are supported?** | iOS and Android. Same quiet experience on both. |
| **I found a bug. How do I report it?** | Email us or open an issue on GitHub. We read everything. |
| **Will you add [feature]?** | Probably not. Small Talk does one thing well. That's the point. |

---

## 6. Implementation Sessions

Each session is designed to be completable in a single agentic context window. Sessions build on each other but are self-contained enough that an agent can pick up from the previous session's deliverables.

---

### Session 1: Project Scaffolding & Configuration

**Goal:** Set up the Astro project with Tailwind, fonts, and base configuration.

**Prerequisites:**
- GitHub account with access to create repos
- Node.js installed locally

**Tasks:**

1. **Create repository**
   - Create `small-talk-website` as a public repo
   - Clone locally
   - Initialize with `.gitignore` for Node projects

2. **Scaffold Astro project**
   ```bash
   npm create astro@latest .
   ```
   - Template: Empty
   - TypeScript: Yes (strict)
   - Install dependencies: Yes

3. **Install and configure TailwindCSS**
   ```bash
   npx astro add tailwind
   ```
   - Configure `tailwind.config.mjs` with custom colors and fonts

4. **Set up self-hosted fonts**
   - Download Lato, Peddana, Caveat from Google Fonts (or use fontsource packages)
   - Convert to WOFF2 format if not already (use google-webfonts-helper or transfonter.org)
   - Place font files in `public/fonts/`
   - Create `src/styles/fonts.css` with `@font-face` declarations
   - Configure font families in Tailwind config
   - Include only the weights/styles actually used (Lato 400/700, Peddana 400, Caveat 400)

5. **Create CSS custom properties**
   - Create `src/styles/theme.css` with color palette variables
   - Create `src/styles/neumorphic.css` with shadow utilities

6. **Set up base layout**
   - Create `src/layouts/BaseLayout.astro`
   - Include meta tags, fonts, global styles
   - Add basic responsive viewport settings

7. **Create placeholder pages**
   - `src/pages/index.astro` — Empty landing page
   - `src/pages/privacy.astro` — Empty privacy page
   - `src/pages/support.astro` — Empty support page

**Deliverables:**
- Working Astro project that builds and runs locally
- Tailwind configured with app color palette
- Self-hosted fonts in `public/fonts/` with `@font-face` declarations
- Base layout with proper meta tags
- Three placeholder pages routing correctly

**Validation:**
- `npm run dev` starts without errors
- Visiting `/`, `/privacy`, `/support` all load
- Fonts load from local `/fonts/` path (verify in Network tab — no requests to fonts.googleapis.com)
- Custom colors available in Tailwind classes

---

### Session 2: Design System & Core Components

**Goal:** Build the reusable components that implement the neumorphic design system.

**Prerequisites:**
- Completed Session 1
- Project runs locally

**Tasks:**

1. **Create neumorphic utility classes**

   Update `src/styles/neumorphic.css`:
   - `.neu-raised` — Raised card/button style
   - `.neu-raised-sm` — Subtle raised style
   - `.neu-pressed` — Inset/pressed style
   - `.neu-flat` — Flat with subtle border
   - `.neu-button` — Interactive button with hover/active states
   - Responsive shadow scales for different screen sizes

2. **Create Button component**

   `src/components/Button.astro`:
   - Primary variant (dark green bg, cream text)
   - Secondary variant (cream bg, dark green text)
   - Neumorphic shadow with hover lift effect
   - Props: `variant`, `href`, `size`

3. **Create Card component**

   `src/components/Card.astro`:
   - Neumorphic raised style
   - Configurable padding
   - Props: `padding`, `class`

4. **Create SectionHeading component**

   `src/components/SectionHeading.astro`:
   - Peddana font title
   - Optional handwritten annotation
   - Centered or left-aligned variants

5. **Create Icon component**

   `src/components/Icon.astro`:
   - SVG icon wrapper
   - Props: `name`, `size`, `class`
   - Include icons: shield (privacy), zap (speed), heart (care), palette (themes)

6. **Create AppStoreBadge component**

   `src/components/AppStoreBadge.astro`:
   - Apple App Store badge
   - Google Play badge
   - Props: `store`, `href`

7. **Create component showcase page** (temporary)

   `src/pages/components.astro`:
   - Display all components for visual testing
   - Verify neumorphic styles render correctly

**Deliverables:**
- Complete set of reusable Astro components
- Neumorphic CSS utilities working correctly
- Component showcase page for visual verification
- Consistent styling across all components

**Validation:**
- All components render without errors
- Neumorphic shadows visible and properly positioned
- Hover/active states work on interactive elements
- Components look correct at mobile and desktop sizes

---

### Session 3: Landing Page Structure

**Goal:** Build the landing page layout with hero, navigation, and footer.

**Prerequisites:**
- Completed Session 2
- All core components working

**Tasks:**

1. **Create Header component**

   `src/components/Header.astro`:
   - Simple, minimal header
   - "Small Talk notebook" branding (Caveat + Peddana)
   - Anchor links: Features, Preview
   - Page links: Privacy, Support
   - Mobile: Horizontal scroll or simplified layout (no hamburger)
   - Optional: Sticky on scroll with subtle shadow

2. **Create Footer component**

   `src/components/Footer.astro`:
   - "For the details that matter." tagline
   - Links: Privacy Policy, Support
   - Copyright year (dynamic)
   - Neumorphic card style or subtle separator
   - Keep it minimal — footer shouldn't compete with content

3. **Create Hero section**

   `src/components/Hero.astro`:
   - Large "Small Talk" (Caveat) + "notebook" (Peddana) branding
   - Tagline: "A quiet place for the people you know."
   - Subtitle: "Just names, notes, and nothing else."
   - Optional anti-feature callout (small, understated):
     "No accounts. No cloud. No sync."
   - App store badges (placeholder hrefs for now)
   - Background: Primary color with decorative circles (like app intro screen)
   - Keep it sparse — resist the urge to add more copy

4. **Update BaseLayout**
   - Include Header
   - Main content slot
   - Include Footer
   - Ensure proper spacing between sections

5. **Build landing page structure**

   Update `src/pages/index.astro`:
   - Hero section
   - Placeholder sections for Features, Preview, Themes
   - Proper section IDs for anchor links

6. **Implement scroll animations**
   - Create `src/scripts/animations.js`
   - IntersectionObserver for fade-in on scroll
   - Apply to section entries
   - Respect `prefers-reduced-motion`

7. **Responsive testing**
   - Verify layout at 320px, 768px, 1024px, 1440px
   - Adjust spacing and typography as needed

**Deliverables:**
- Complete landing page structure
- Working header with navigation
- Polished hero section matching app aesthetic
- Footer with links
- Scroll animations (subtle fade-in)
- Fully responsive layout

**Validation:**
- Navigation anchor links scroll smoothly to sections
- Hero matches the app's intro screen aesthetic
- Animations trigger on scroll (unless reduced motion)
- No horizontal overflow at any viewport size
- Footer links work (even if pages are empty)

---

### Session 4: Landing Page Content Sections

**Goal:** Complete the landing page with features, app preview, and theme showcase.

**Prerequisites:**
- Completed Session 3
- Landing page structure in place

**Tasks:**

1. **Create FeatureCard component**

   `src/components/FeatureCard.astro`:
   - Neumorphic card style
   - Icon at top
   - Title (Peddana)
   - Description (Lato)
   - Props: `icon`, `title`, `description`

2. **Build Features section**

   `src/components/FeaturesSection.astro`:
   - Section heading (keep it minimal or skip entirely — let cards speak)
   - 3-4 feature cards in responsive grid
   - Use "what it doesn't do" framing from Section 5:
     - **Truly private** (shield icon) — Nothing leaves your phone.
     - **Just one thing** (check icon) — Add people. Write notes. That's it.
     - **No demands** (moon/quiet icon) — No streaks. No reminders. No guilt.
     - **Make it yours** (palette icon) — Choose a palette that feels like you.

3. **Create PhoneMockup component**

   `src/components/PhoneMockup.astro`:
   - CSS-based phone frame (rounded rect with notch)
   - Slot for screenshot image
   - Optional: Shadow beneath phone
   - Responsive sizing

4. **Build Preview section**

   `src/components/PreviewSection.astro`:
   - Section heading
   - Phone mockup with screenshot
   - Option for multiple screenshots (carousel or grid)
   - Brief caption below

5. **Build Themes section** (optional but recommended)

   `src/components/ThemesSection.astro`:
   - Minimal heading or none — let the palettes speak
   - Display 3-4 color palette swatches
   - Palette names (Morning Window, Late Afternoon, etc.)
   - Small note: "One theme free. Unlock all with a one-time purchase."
   - Interactive: clicking a palette could change page theme (stretch goal)

6. **Create placeholder images**
   - Create `public/images/` directory
   - Add placeholder screenshot (or actual if available)
   - Add any decorative assets

7. **Integrate sections into landing page**
   - Update `src/pages/index.astro`
   - Proper section ordering and spacing
   - Verify all anchor links work

8. **Final landing page polish**
   - Consistent spacing between sections
   - Typography hierarchy is clear
   - All interactive elements have hover states

**Deliverables:**
- Complete landing page with all content sections
- Feature cards with icons and descriptions
- Phone mockup component (ready for real screenshots)
- Theme showcase section
- Polished, cohesive visual design

**Validation:**
- All sections visible and properly styled
- Feature cards display in responsive grid
- Phone mockup looks like a real device
- Page feels cohesive with app's aesthetic
- Performance: Page loads quickly (check Lighthouse)

---

### Session 5: Privacy Policy Page

**Goal:** Create a well-formatted, legally appropriate privacy policy.

**Prerequisites:**
- Completed Session 4 (or at minimum Session 3 for layout)
- Understanding of app's data practices

**Tasks:**

1. **Create prose styling**

   `src/styles/prose.css`:
   - Typography for long-form content
   - Headings (h2, h3) in Peddana
   - Body paragraphs in Lato
   - Bullet lists with proper spacing
   - Blockquotes styled for callouts

2. **Create ContentLayout component**

   `src/layouts/ContentLayout.astro`:
   - Extends BaseLayout
   - Narrower max-width for readability (prose width)
   - Title heading
   - Last updated date
   - Back to home link

3. **Write privacy policy content**

   `src/content/privacy-policy.md` (or inline in page):

   **Tone:** Write like a human. Short sentences. Plain language. This should feel like relief, not legal obligation.

   Sections to include:
   - **The short version** — Lead with the key point: "Your notes never leave your device. We can't see them. No one can."
   - **What we collect** — Nothing. No accounts, no tracking, no analytics.
   - **How your data is stored** — On your device, encrypted. (Avoid jargon.)
   - **Third-party services** — None.
   - **Data sharing** — Never.
   - **Your control** — Delete everything anytime. It's your notebook.
   - **Children's privacy** — Not directed at children under 13
   - **Changes to this policy** — We'll update this page. That's it.
   - **Questions?** — Email us.

4. **Build privacy page**

   Update `src/pages/privacy.astro`:
   - Use ContentLayout
   - Render privacy policy content
   - Proper heading hierarchy for accessibility
   - Last updated date

5. **Add effective date**
   - Include "Last Updated: [Date]" at top
   - Consider versioning for future updates

**Deliverables:**
- Complete privacy policy page
- Well-formatted, readable content
- Legally appropriate for App Store/Play Store
- Consistent styling with rest of site

**Validation:**
- All sections present and complete
- Typography is readable (line length, spacing)
- Page is accessible (heading hierarchy, contrast)
- Links back to home page work
- Content accurately reflects app's data practices

---

### Session 6: Support Page & Final Polish

**Goal:** Complete the support page and polish the entire site for launch.

**Prerequisites:**
- Completed Session 5
- All major pages functional

**Tasks:**

1. **Write FAQ content**

   Use the reframed FAQ from Section 5. Key principles:
   - Lead with value, not limitations
   - Keep answers short and conversational
   - Embrace the "we don't do that" positioning

   Questions to include:
   - "Where is my data stored?"
   - "Can I take my notes with me?"
   - "How much does it cost?"
   - "What platforms are supported?"
   - "I found a bug. How do I report it?"
   - "Will you add [feature]?"

2. **Create FAQ component**

   `src/components/FAQ.astro`:
   - Accordion-style expandable questions
   - Neumorphic styling
   - Accessible keyboard navigation
   - Smooth expand/collapse animation

3. **Build support page**

   Update `src/pages/support.astro`:
   - Section: FAQ with common questions
   - Section: Contact (email address)
   - Optional: Link to GitHub Issues for bug reports
   - Use ContentLayout for consistency

4. **SEO & meta tags**

   Update all pages:
   - Title tags (unique per page)
   - Meta descriptions
   - Open Graph tags (og:title, og:description, og:image)
   - Twitter card tags
   - Canonical URLs

5. **Create OG image**
   - Design a simple 1200x630 image for social sharing
   - App branding + tagline
   - Save to `public/og-image.png`

6. **Favicon & app icons**
   - Add favicon.ico
   - Add apple-touch-icon.png
   - Add site.webmanifest (basic)

7. **Accessibility audit**
   - Run axe or Lighthouse accessibility check
   - Fix any issues (contrast, alt text, labels)
   - Ensure keyboard navigation works
   - Test with screen reader (basic check)

8. **Performance optimization**
   - Optimize images (WebP format, proper sizing)
   - Verify no layout shift (CLS)
   - Check Lighthouse performance score

9. **Cross-browser testing**
   - Test in Chrome, Firefox, Safari
   - Test on iOS Safari and Android Chrome
   - Fix any rendering issues

10. **Final content review**
    - Proofread all copy
    - Verify all links work
    - Check responsive layouts one more time

**Deliverables:**
- Complete support page with FAQ
- All meta tags and SEO in place
- Favicon and OG image
- Accessibility issues resolved
- Performance optimized
- Cross-browser tested

**Validation:**
- Lighthouse scores: Performance >90, Accessibility 100, SEO >90
- All pages load without console errors
- FAQ accordion works with keyboard
- Social sharing preview looks correct (use ogimage.dev or similar)
- Site works on mobile devices

---

### Session 7: Deployment & Launch

**Goal:** Deploy the website and configure for production.

**Prerequisites:**
- Completed Session 6
- All content and polish complete
- GitHub repository ready

**Tasks:**

1. **Configure Astro for static output**

   `astro.config.mjs`:
   ```javascript
   export default defineConfig({
     site: 'https://yourusername.github.io',
     base: '/small-talk-website', // if using project pages
     output: 'static',
   });
   ```

2. **Set up GitHub Pages deployment**

   Option A: GitHub Actions (recommended)
   - Create `.github/workflows/deploy.yml`
   - Use Astro's official GitHub Pages action
   - Triggers on push to main branch

   Option B: Manual deployment
   - Build locally: `npm run build`
   - Push `dist/` to `gh-pages` branch

3. **Configure custom domain** (optional)
   - Add CNAME file to `public/` if using custom domain
   - Configure DNS records
   - Enable HTTPS in GitHub Pages settings

4. **Update app store URLs**
   - Once apps are published, update App Store badge hrefs
   - Update Play Store badge hrefs

5. **Verify production deployment**
   - Check all pages load correctly
   - Verify HTTPS is working
   - Test all links
   - Check OG image appears in social previews

6. **Set up redirects** (if needed)
   - `/privacy-policy` → `/privacy`
   - Any other legacy URLs

7. **Document the website**
   - Update main repo README with website link
   - Add website repo to Small Talk project documentation
   - Note deployment process for future updates

8. **Create simple update workflow**
   - Document how to update content
   - Document how to deploy changes
   - Note any manual steps required

**Deliverables:**
- Live website at GitHub Pages URL
- Automated deployment via GitHub Actions
- All links updated and working
- Documentation for future updates

**Validation:**
- Site accessible at public URL
- HTTPS working correctly
- All pages render correctly in production
- Deployment triggers automatically on push
- App store links ready (or clearly marked as placeholder)

---

## 7. Asset Checklist

Before starting implementation, gather or create these assets:

### Required

- [ ] App icon (PNG, 512x512 minimum)
- [ ] At least 2 app screenshots
- [ ] Privacy policy content (text)
- [ ] Support email address
- [ ] App Store URL (or "Coming Soon" strategy)
- [ ] Play Store URL (or "Coming Soon" strategy)

### Recommended

- [ ] 3-5 app screenshots showing different screens
- [ ] OG image for social sharing (1200x630)
- [ ] Favicon (can derive from app icon)

### Optional

- [ ] App demo video/GIF
- [ ] Decorative illustrations
- [ ] Custom icons (or use Lucide/Heroicons)

---

## 8. Future Enhancements

After v1 launch, consider:

1. **Theme switcher** — Let visitors preview different color palettes
2. **App demo** — Embedded video or interactive prototype
3. **Blog/Updates** — Changelog or development blog
4. **Localization** — Multi-language support
5. **Analytics** — Privacy-respecting analytics (Plausible, Fathom)
6. **Press kit** — Downloadable assets for reviews/press

---

## 9. Reference

### App Design Documents

- `implementation_plans/design_requirements.md` — Full product spec
- `small_talk_notebook/lib/config/theme/color_palette.dart` — All color palettes
- `small_talk_notebook/lib/config/theme/typography.dart` — Font configurations
- `small_talk_notebook/lib/config/theme/neumorphic.dart` — Shadow utilities

### External Resources

- [Astro Documentation](https://docs.astro.build)
- [TailwindCSS Documentation](https://tailwindcss.com/docs)
- [google-webfonts-helper](https://gwfh.mranftl.com/fonts) — Download Google Fonts for self-hosting with CSS snippets
- [Transfonter](https://transfonter.org) — Convert fonts to WOFF2 format
- [Apple App Store Marketing Guidelines](https://developer.apple.com/app-store/marketing/guidelines/)
- [Google Play Badge Guidelines](https://play.google.com/intl/en_us/badges/)

---

## 10. Brand Guidelines Quick Reference

A summary for quick reference during implementation.

### Target Audience

- **Forgetful introverts** — Care deeply, struggle to remember
- **Social connectors** — Many relationships, want to be more thoughtful

### Voice & Tone

| Do | Don't |
|----|-------|
| Short sentences. Fragments OK. | Long explanations |
| Plain, conversational language | Jargon or technical terms |
| Confident but humble | Hype or superlatives |
| "We don't do X" (embrace limitations) | Apologize for missing features |

### Words to Avoid

- **Productivity:** optimize, hack, leverage, 10x, boost, supercharge
- **Corporate:** solutions, empower, synergy, leverage, streamline
- **Hype:** revolutionary, game-changing, amazing, incredible, powerful

### Key Messages

1. **Simplicity is the feature.** One thing, done well.
2. **Privacy by design.** No accounts, no cloud, no tracking.
3. **No demands.** No streaks, no notifications, no guilt.
4. **Generous free.** Everything you need is free. Pay once for extras.

### Desired Feelings

- **Trust** — "This feels safe and well-made."
- **Relief** — "Finally, something simple that respects me."

---

## Revision History

| Date | Change |
|------|--------|
| 2026-02-05 | Initial website implementation plan |
| 2026-02-05 | Added brand guidelines, revised copy for calm/minimal tone, reframed features around simplicity |
| 2026-02-05 | Changed to self-hosted fonts for privacy alignment and GDPR compliance |
