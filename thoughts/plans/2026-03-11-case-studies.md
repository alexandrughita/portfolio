# Case Studies Section - Implementation Plan

## Overview

Add a "Studiu de caz" section to the portfolio homepage and create two detailed English-language case study pages for e-Factura and TrackGlow. Pages will feature scroll-triggered animations (AOS library), image carousels (Swiper.js), and showcase the developer's ability to build production apps using exclusively free-tier infrastructure.

## Current State

- Portfolio is a static HTML/CSS/JS site at `/Users/macbookuser/alex/portfolio/`
- Hosted on GitHub Pages at `alexandrughita.eu`
- Homepage has a hidden `#portofoliu` section (display:none) with 3 placeholder project cards
- Design system: Bricolage Grotesque font, gold accent `#f4a825`, CSS variables, scroll reveal via Intersection Observer
- Existing `/e-factura/index.html` is a Romanian marketing/service page — untouched
- No build process, pure HTML/CSS/JS

## Desired End State

1. Homepage `#portofoliu` section is visible, renamed to "studiu de caz", contains 2 cards linking to detail pages
2. `/studiu-de-caz/e-factura/index.html` — full English case study page
3. `/studiu-de-caz/trackglow/index.html` — full English case study page
4. Both pages use Swiper.js for screenshot carousels and AOS for scroll animations
5. Placeholder screenshot slots ready to be swapped with real images
6. Fully responsive, GA4 tracked, consistent design language

### Verification:
- Open `index.html` locally — "studiu de caz" section visible with 2 cards
- Click each card → navigates to case study page
- Carousel navigates with arrows/dots, auto-advances
- Scroll animations trigger on scroll
- Mobile responsive at 600px and 900px breakpoints
- All links work (live project, back to portfolio, contact)

## What We're NOT Doing

- Not touching the existing `/e-factura/index.html` service page
- Not adding i18n/language switching (planned for future)
- Not adding a CMS or build process
- Not creating real screenshots yet (Phase 5 handles that separately)

## External Libraries (CDN)

- **Swiper.js** (v11) — carousel/slideshow with touch support, pagination, autoplay
  - CSS: `https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.css`
  - JS: `https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.js`
- **AOS** (Animate On Scroll v2) — scroll-triggered entrance animations
  - CSS: `https://cdn.jsdelivr.net/npm/aos@2.3.4/dist/aos.css`
  - JS: `https://cdn.jsdelivr.net/npm/aos@2.3.4/dist/aos.js`

---

## Phase 1: Shared Styles + Case Study CSS

### Overview
Add all new CSS classes to `style.css` for the updated portfolio cards and case study pages.

### Changes Required:

#### 1. Update `portfolio/style.css`

**Add at the end of the file**, before the responsive section:

```css
/* ── Case Study Cards (Homepage) ─────────────────────────── */

.porto-grid {
  /* Change from 3-col to 2-col for case study cards */
  grid-template-columns: repeat(2, 1fr);
}

.porto-card {
  /* Already exists — add thumbnail image support */
}

.porto-thumb {
  aspect-ratio: 16 / 9;
  background: #eceae6;
  overflow: hidden;
  position: relative;
}

.porto-thumb img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s ease;
}

.porto-card:hover .porto-thumb img {
  transform: scale(1.03);
}

.porto-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
  margin-top: 10px;
}

.porto-tags span {
  font-size: 11px;
  font-weight: 500;
  padding: 3px 9px;
  border-radius: 4px;
  border: 1px solid var(--border);
  color: var(--muted);
  background: rgba(0,0,0,0.02);
}

.porto-tags .tag-free {
  border-color: rgba(34, 197, 94, 0.3);
  color: #15803d;
  background: rgba(34, 197, 94, 0.06);
}

/* ── Case Study Page Styles ──────────────────────────────── */

/* These are loaded via style.css on case study pages too */

.cs-topbar {
  border-bottom: 1px solid var(--border);
  background: var(--bg);
  position: sticky;
  top: 0;
  z-index: 100;
}

.cs-topbar-inner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 0;
}

.cs-topbar .nav-logo {
  font-size: 18px;
  font-weight: 700;
  color: var(--text);
  text-decoration: none;
  letter-spacing: -0.02em;
}

.cs-topbar .nav-dot { color: var(--gold); }

.cs-back {
  text-decoration: none;
  color: var(--muted);
  font-size: 14px;
  font-weight: 400;
  display: inline-flex;
  align-items: center;
  gap: 6px;
  transition: color 0.15s;
}

.cs-back:hover { color: var(--text); }

/* Hero */
.cs-hero {
  padding: 80px 0 48px;
  border-bottom: 1px solid var(--border);
}

.cs-badge {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-size: 13px;
  font-weight: 600;
  padding: 7px 14px;
  border-radius: 999px;
  border: 1px solid rgba(244, 168, 37, 0.35);
  background: rgba(244, 168, 37, 0.08);
  color: #7a5311;
  margin-bottom: 20px;
}

.cs-hero h1 {
  font-size: clamp(36px, 5vw, 64px);
  font-weight: 800;
  line-height: 1.08;
  letter-spacing: -0.03em;
  margin-bottom: 16px;
}

.cs-hero .lead {
  font-size: 18px;
  color: var(--muted);
  max-width: 680px;
  line-height: 1.7;
  font-weight: 300;
  margin-bottom: 28px;
}

.cs-hero-actions {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}

/* Sections */
.cs-section {
  padding: 72px 0;
  border-bottom: 1px solid var(--border);
}

.cs-section:last-of-type {
  border-bottom: none;
}

.cs-section.alt {
  background: var(--bg-alt);
}

.cs-section h2 {
  font-size: clamp(28px, 3.5vw, 44px);
  font-weight: 800;
  letter-spacing: -0.025em;
  margin-bottom: 12px;
}

.cs-section .section-sub {
  font-size: 0.45em;
  font-weight: 400;
  color: var(--subtle);
}

.cs-section-intro {
  font-size: 16px;
  color: var(--muted);
  line-height: 1.7;
  max-width: 640px;
  font-weight: 300;
  margin-bottom: 36px;
}

/* Problem / Solution cards */
.cs-problem-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}

.cs-card {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 32px;
}

.cs-card.dark {
  background: var(--text);
  color: #fff;
  border: none;
}

.cs-card.dark p,
.cs-card.dark li {
  color: rgba(255,255,255,0.65);
}

.cs-card h3 {
  font-size: 20px;
  font-weight: 700;
  margin-bottom: 12px;
  letter-spacing: -0.02em;
}

.cs-card ul {
  list-style: none;
  padding: 0;
}

.cs-card ul li {
  font-size: 15px;
  color: var(--muted);
  line-height: 1.7;
  padding: 6px 0;
  padding-left: 16px;
  position: relative;
}

.cs-card ul li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 14px;
  width: 5px;
  height: 5px;
  border-radius: 50%;
  background: var(--gold);
}

.cs-card.dark ul li::before {
  background: var(--gold);
}

/* Screenshots / Carousel */
.cs-carousel {
  margin-top: 36px;
}

.cs-carousel .swiper {
  border-radius: 12px;
  overflow: hidden;
  border: 1px solid var(--border);
}

.cs-carousel .swiper-slide {
  aspect-ratio: 16 / 9;
  background: #eceae6;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.cs-carousel .swiper-slide img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.cs-carousel .swiper-slide .placeholder {
  font-size: 15px;
  color: #b0ada8;
  font-weight: 500;
}

.cs-carousel .swiper-pagination-bullet-active {
  background: var(--gold) !important;
}

.cs-carousel .swiper-button-next,
.cs-carousel .swiper-button-prev {
  color: var(--gold) !important;
}

.cs-carousel .swiper-button-next::after,
.cs-carousel .swiper-button-prev::after {
  font-size: 20px !important;
}

.cs-slide-caption {
  text-align: center;
  font-size: 13px;
  color: var(--muted);
  font-weight: 300;
  margin-top: 12px;
  padding: 0 20px;
}

/* Tech Stack */
.cs-tech-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 14px;
}

.cs-tech-card {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 10px;
  padding: 20px 22px;
}

.cs-tech-card h4 {
  font-size: 12px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  color: var(--subtle);
  margin-bottom: 10px;
}

.cs-tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.cs-tech-tag {
  font-size: 13px;
  font-weight: 500;
  padding: 5px 12px;
  border-radius: 6px;
  border: 1px solid var(--border);
  color: var(--text);
  background: var(--bg);
}

.cs-tech-tag.free {
  border-color: rgba(34, 197, 94, 0.35);
  color: #15803d;
  background: rgba(34, 197, 94, 0.06);
  position: relative;
}

.cs-tech-tag.free::after {
  content: 'FREE';
  font-size: 8px;
  font-weight: 700;
  letter-spacing: 0.05em;
  color: #15803d;
  margin-left: 5px;
}

/* Features grid */
.cs-features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 14px;
}

.cs-feature {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 10px;
  padding: 24px;
}

.cs-feature h3 {
  font-size: 17px;
  font-weight: 700;
  margin-bottom: 8px;
}

.cs-feature p {
  font-size: 14px;
  color: var(--muted);
  line-height: 1.65;
  font-weight: 300;
}

/* Architecture */
.cs-arch {
  background: var(--text);
  color: #fff;
  border-radius: 12px;
  padding: 36px;
  margin-top: 24px;
}

.cs-arch h3 {
  font-size: 20px;
  font-weight: 700;
  margin-bottom: 20px;
  color: #fff;
}

.cs-arch-flow {
  display: flex;
  align-items: center;
  gap: 12px;
  flex-wrap: wrap;
  justify-content: center;
}

.cs-arch-step {
  background: rgba(255,255,255,0.08);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 8px;
  padding: 14px 18px;
  text-align: center;
  min-width: 120px;
}

.cs-arch-step strong {
  display: block;
  font-size: 14px;
  font-weight: 600;
  margin-bottom: 4px;
}

.cs-arch-step span {
  font-size: 12px;
  color: rgba(255,255,255,0.5);
}

.cs-arch-arrow {
  color: var(--gold);
  font-size: 20px;
  font-weight: 700;
}

/* Cost summary */
.cs-cost {
  background: rgba(34, 197, 94, 0.06);
  border: 1px solid rgba(34, 197, 94, 0.2);
  border-radius: 12px;
  padding: 28px 32px;
  margin-top: 32px;
  text-align: center;
}

.cs-cost-title {
  font-size: 14px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  color: #15803d;
  margin-bottom: 6px;
}

.cs-cost-amount {
  font-size: 48px;
  font-weight: 800;
  color: #15803d;
  letter-spacing: -0.03em;
}

.cs-cost-note {
  font-size: 14px;
  color: var(--muted);
  margin-top: 6px;
  font-weight: 300;
}

/* CTA */
.cs-cta {
  padding: 72px 0;
}

.cs-cta-box {
  background: var(--text);
  color: #fff;
  border-radius: 14px;
  padding: 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 24px;
  flex-wrap: wrap;
}

.cs-cta-box h2 {
  font-size: clamp(24px, 3vw, 36px);
  font-weight: 800;
  letter-spacing: -0.025em;
  margin-bottom: 8px;
  color: #fff;
}

.cs-cta-box p {
  color: rgba(255,255,255,0.6);
  font-size: 15px;
  max-width: 500px;
  font-weight: 300;
  line-height: 1.7;
}

.cs-cta-actions {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
  flex-shrink: 0;
}

.cs-cta-actions .btn-primary {
  background: var(--gold);
  color: #111;
}

.cs-cta-actions .btn-outline {
  border: 1px solid rgba(255,255,255,0.3);
  color: #fff;
  background: transparent;
}

/* ── Case Study Responsive ───────────────────────────────── */

@media (max-width: 900px) {
  .cs-problem-grid {
    grid-template-columns: 1fr;
  }
  .cs-arch-flow {
    flex-direction: column;
  }
  .cs-arch-arrow {
    transform: rotate(90deg);
  }
}

@media (max-width: 600px) {
  .cs-hero { padding: 56px 0 36px; }
  .cs-section { padding: 48px 0; }
  .cs-cta { padding: 48px 0; }
  .cs-cta-box {
    flex-direction: column;
    align-items: flex-start;
    padding: 28px;
  }
  .cs-arch { padding: 24px; }
  .cs-card { padding: 22px; }
}
```

### Success Criteria:
- [ ] All new CSS classes are added to `style.css`
- [ ] No existing styles are broken (visual check of homepage)
- [ ] Responsive breakpoints at 900px and 600px work correctly

---

## Phase 2: Homepage Portofoliu → Studiu de Caz

### Overview
Un-hide the existing Portofoliu section, change heading to "studiu de caz", replace the 3 placeholder cards with 2 case study cards.

### Changes Required:

#### 1. `portfolio/index.html` — Portofoliu section (lines 228-277)

Remove `style="display:none"` from the section.

Replace heading:
```html
<h2 class="section-heading">studiu de caz <span class="section-sub">/ proiecte personale</span></h2>
<p class="section-intro">Proiecte de la zero la producție — de la idee la aplicație live, cu infrastructură 100% gratuită.</p>
```

Replace the 3 existing `porto-card` elements with 2 new ones:
```html
<div class="porto-grid">

  <a class="porto-card" href="/studiu-de-caz/e-factura/">
    <div class="porto-thumb">
      <img src="/studiu-de-caz/e-factura/thumb.webp" alt="e-Factura app screenshot" loading="lazy" onerror="this.style.display='none'" />
    </div>
    <div class="porto-body">
      <div class="porto-title-row">
        <h3>e-Factura</h3>
        <svg class="porto-link-icon" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
      </div>
      <p class="porto-cat">Laravel / Alpine.js / Fly.io</p>
      <p class="porto-desc">Aplicație web pentru firmele mici din România — facturi electronice conforme ANAF, generate și trimise simplu, fără complicații.</p>
      <div class="porto-tags">
        <span>Laravel 12</span>
        <span>Tailwind CSS</span>
        <span class="tag-free">Fly.io Free</span>
        <span class="tag-free">SQLite</span>
      </div>
    </div>
  </a>

  <a class="porto-card" href="/studiu-de-caz/trackglow/">
    <div class="porto-thumb">
      <img src="/studiu-de-caz/trackglow/thumb.webp" alt="TrackGlow app screenshot" loading="lazy" onerror="this.style.display='none'" />
    </div>
    <div class="porto-body">
      <div class="porto-title-row">
        <h3>TrackGlow</h3>
        <svg class="porto-link-icon" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
      </div>
      <p class="porto-cat">Next.js / Python / AI Audio</p>
      <p class="porto-desc">Platformă SaaS de mastering audio cu AI. Încarci un beat, alegi un preset de artist și primești un master studio-quality în minute.</p>
      <div class="porto-tags">
        <span>Next.js 16</span>
        <span>Python</span>
        <span class="tag-free">Vercel Free</span>
        <span class="tag-free">Supabase Free</span>
        <span class="tag-free">R2 Free</span>
      </div>
    </div>
  </a>

</div>
```

Also update the `porto-cta`:
```html
<div class="porto-cta">
  <p>Fiecare proiect rulează pe infrastructură 100% gratuită.</p>
  <a href="#contact" class="btn btn-primary">Hai să vorbim →</a>
</div>
```

#### 2. Update scroll reveal selectors in JS (line ~444)

Add `.porto-thumb` and `.porto-tags` to the reveal selectors if needed (existing `.porto-card` selector already covers cards).

#### 3. Update nav

Add a "Studiu de caz" link in the nav `<ul>`:
```html
<li><a href="#portofoliu">Studiu de caz</a></li>
```

### Success Criteria:
- [ ] Homepage shows "studiu de caz" section with 2 cards
- [ ] Cards link to `/studiu-de-caz/e-factura/` and `/studiu-de-caz/trackglow/`
- [ ] Section has scroll reveal animations
- [ ] Responsive: cards stack on mobile (1-col under 600px)
- [ ] Nav link scrolls to the section

---

## Phase 3: e-Factura Case Study Page

### Overview
Create `/studiu-de-caz/e-factura/index.html` — a comprehensive English-language case study.

### File: `portfolio/studiu-de-caz/e-factura/index.html`

#### Page Structure:

1. **Topbar** — Logo (links to /) + "Back to portfolio" link
2. **Hero** — Badge "Case Study · Web App", title "e-Factura", lead text, buttons (View Live + View Source)
3. **Screenshots Carousel** — Swiper.js with 5 placeholder slides:
   - Dashboard view
   - Invoice creation form
   - Invoice PDF preview
   - Client management
   - XML export view
4. **The Problem** — 2-col grid: problem card (dark) + solution card
   - Problem: Romanian SMBs face complex, expensive e-invoicing. ANAF's system is confusing. Most tools cost money and are overbuilt.
   - Solution: A free, simple web app that handles the entire flow — create invoice, generate CIUS-RO XML, export PDF, email to client.
5. **Tech Stack** — Grid of categorized tech tags with FREE badges:
   - Backend: Laravel 12, PHP 8.4
   - Frontend: Tailwind CSS v3, Alpine.js, Vite
   - Database: SQLite (FREE), PostgreSQL (prod)
   - PDF: DOMPDF
   - Hosting: Fly.io (FREE), Docker
   - SSL: Let's Encrypt (FREE)
6. **Key Features** — Grid of feature cards:
   - UBL 2.1 XML generation (CIUS-RO standard)
   - ANAF CUI auto-lookup (company data from tax ID)
   - Multi-currency (RON/EUR) with VAT calculation
   - Invoice series with auto-numbering
   - PDF export & email to clients
   - Company management with logo upload
   - GDPR data export
   - Responsive — works on any device
7. **Architecture** — Dark box with flow diagram:
   `Browser → Laravel (Fly.io) → SQLite → UBL XML / PDF / Email`
8. **Monthly Cost** — Green highlight box: "$0/month" with note about free tier
9. **CTA** — Dark box with "Like what you see?" + email/WhatsApp buttons

#### Swiper Config:
```js
new Swiper('.swiper', {
  loop: true,
  autoplay: { delay: 4000, disableOnInteraction: true },
  pagination: { el: '.swiper-pagination', clickable: true },
  navigation: { nextEl: '.swiper-button-next', prevEl: '.swiper-button-prev' },
  effect: 'slide',
  speed: 500,
});
```

#### AOS Config:
```js
AOS.init({ duration: 700, once: true, offset: 60 });
```

Elements get `data-aos="fade-up"` with staggered `data-aos-delay`.

### Success Criteria:
- [ ] Page loads at `/studiu-de-caz/e-factura/`
- [ ] Swiper carousel works (arrows, dots, autoplay)
- [ ] AOS scroll animations trigger
- [ ] All sections render correctly
- [ ] FREE tags visible on tech stack
- [ ] "$0/month" cost box prominent
- [ ] Responsive at all breakpoints
- [ ] GA4 tracking fires
- [ ] "View Live" links to https://e.alexandrughita.eu

---

## Phase 4: TrackGlow Case Study Page

### Overview
Create `/studiu-de-caz/trackglow/index.html` — same structure, different content.

### File: `portfolio/studiu-de-caz/trackglow/index.html`

#### Page Structure:

1. **Topbar** — Same as e-Factura
2. **Hero** — Badge "Case Study · SaaS Platform", title "TrackGlow", lead text, buttons (View Live + View Source)
3. **Screenshots Carousel** — 6 placeholder slides:
   - Landing page with video hero
   - Upload & preset selection
   - Mastering in progress
   - Completed job with audio player
   - Artist preset grid
   - Admin dashboard
4. **The Problem** — 2-col:
   - Problem: Professional mastering costs $50-200/track. Requires expensive software (iZotope, FabFilter) and trained ears. Homestudio producers and rappers can't afford it.
   - Solution: Upload a track, pick an artist preset (Drake, Travis Scott, The Weeknd...), get AI-mastered output in minutes. Free to use, studio-quality results.
5. **Tech Stack** — Grid with FREE badges:
   - Frontend: Next.js 16, React 19, TypeScript, Tailwind CSS v4
   - Auth: NextAuth v5 (Google OAuth + credentials)
   - Database: Supabase PostgreSQL (FREE) + Prisma v6
   - Storage: Cloudflare R2 (FREE)
   - Queue: Upstash Redis (FREE)
   - Audio Engine: Python 3.11, matchering, Spotify pedalboard, FFmpeg
   - Frontend Hosting: Vercel (FREE)
   - Worker Hosting: Fly.io (FREE)
   - Email: Resend (FREE)
6. **Key Features** — Grid:
   - 11 artist presets + 4 style presets
   - 2-stage audio pipeline (EQ matching + character effects)
   - Intensity slider (0-100% wet/dry)
   - Custom reference track upload
   - Version retry system (try 3 presets, compare, download best)
   - BPM & musical key detection
   - GDPR cookie consent + GA4
   - Admin dashboard with feature toggles
   - Blog system with scheduled publishing
   - SEO: JSON-LD, sitemap, Open Graph
7. **Architecture** — Dark box with pipeline:
   `Upload → Presigned S3 PUT → Redis Queue → Python Worker (matchering + pedalboard) → R2 Output → Poll & Download`
8. **Monthly Cost** — "$0/month" — 6 free services working together
9. **CTA** — Same structure

### Success Criteria:
- [ ] Page loads at `/studiu-de-caz/trackglow/`
- [ ] Same carousel, animation, responsive behavior as e-Factura page
- [ ] Architecture pipeline reads clearly
- [ ] All 6 free-tier services highlighted
- [ ] "View Live" links to https://trackglow.in

---

## Phase 5: Screenshots

### Overview
Take real screenshots from both live apps and place them in the correct directories.

### Process:
1. Navigate to https://e.alexandrughita.eu — take screenshots of each view
2. Navigate to https://trackglow.in — take screenshots of each view
3. Convert to .webp, optimize, place in:
   - `portfolio/studiu-de-caz/e-factura/` (screenshots + thumb.webp)
   - `portfolio/studiu-de-caz/trackglow/` (screenshots + thumb.webp)
4. Update `<img>` src attributes in both pages
5. Update homepage card thumbnails

### Screenshots needed:

**e-Factura** (5 screenshots):
1. `dash.webp` — Dashboard overview
2. `invoice-create.webp` — Invoice creation form
3. `invoice-pdf.webp` — PDF preview
4. `clients.webp` — Client list
5. `thumb.webp` — Best screenshot for card thumbnail (cropped dashboard)

**TrackGlow** (6 screenshots):
1. `landing.webp` — Landing page hero
2. `upload.webp` — Upload + preset selection
3. `processing.webp` — Job in progress
4. `completed.webp` — Completed with audio player
5. `presets.webp` — Preset grid
6. `thumb.webp` — Best screenshot for card thumbnail (cropped landing)

### Success Criteria:
- [ ] All placeholder slides replaced with real screenshots
- [ ] Homepage thumbnails show actual app previews
- [ ] Images are .webp, reasonably optimized
- [ ] All images have meaningful alt text

---

## File Structure (Final)

```
portfolio/
├── index.html                          (modified — Portofoliu section updated)
├── style.css                           (modified — new case study styles)
├── studiu-de-caz/
│   ├── e-factura/
│   │   ├── index.html                  (NEW — case study page)
│   │   ├── thumb.webp                  (NEW — card thumbnail)
│   │   ├── dash.webp                   (NEW — screenshot)
│   │   ├── invoice-create.webp         (NEW)
│   │   ├── invoice-pdf.webp            (NEW)
│   │   └── clients.webp               (NEW)
│   └── trackglow/
│       ├── index.html                  (NEW — case study page)
│       ├── thumb.webp                  (NEW — card thumbnail)
│       ├── landing.webp                (NEW — screenshot)
│       ├── upload.webp                 (NEW)
│       ├── processing.webp             (NEW)
│       ├── completed.webp              (NEW)
│       └── presets.webp                (NEW)
├── e-factura/
│   └── index.html                      (UNTOUCHED — service page)
└── test/
    └── index.html                      (UNTOUCHED)
```

## References

- Portfolio repo: `/Users/macbookuser/alex/portfolio/`
- e-Factura app: `/Users/macbookuser/alex/e-factura/` (live: https://e.alexandrughita.eu)
- TrackGlow app: `/Users/macbookuser/typemaster/` (live: https://trackglow.in)
- Swiper.js docs: https://swiperjs.com/
- AOS docs: https://michalsnik.github.io/aos/
