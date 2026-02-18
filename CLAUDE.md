# CLAUDE.md — Weil Germany Microsite (de.weil.com)

## Project Overview

WordPress microsite for **Weil, Gotshal & Manges LLP** (international law firm, HQ New York) to establish a dedicated German online presence at **de.weil.com**.

- **Client**: Weil, Gotshal & Manges LLP (Frankfurt office)
- **Client Contact**: Dr. Sepita Ansari
- **Developer**: Kamanin IT Solutions
- **Go-Live Target**: April 2026 (Phase 1 — standalone, no integrations)
- **Phase 2**: From May 2026 — Sitecore API integration, ATS connection

## Why This Project Exists

Weil's global site (weil.com) runs on Sitecore CMS managed by the US team. The German office has no control over content updates — everything goes through a global CMS ticketing process. This kills local SEO visibility and slows down marketing/HR. The solution: a standalone German subdomain on WordPress with local editorial control, while maintaining brand consistency with the global site.

## Tech Stack

- **CMS**: WordPress (Gutenberg editor, custom theme)
- **Hosting**: WPEngine (US-based, managed by Weil's US IT)
- **Multilingual**: WPML plugin (DE + EN)
- **Custom Fields**: ACF Pro (Advanced Custom Fields)
- **Domain**: de.weil.com (subdomain of weil.com, DNS managed by US IT)
- **Parent Site**: weil.com (Sitecore CMS — XP, XM, or XM Cloud — version unknown)

## Site Structure (8 Modules)

### 1. HOME
- Hero section with local imagery
- Key USP / Value Proposition (static)
- Deal Highlights / Selected References (Custom Post Type with Practice Area + year filters)

### 2. TEAM / PEOPLE
- Attorney profiles (Partner, Counsel, Associates) — replicate weil.com/people functionality
- Search + filter (Practice, Title, Office)
- Video integration on profile pages (Vimeo/YouTube, 2-click GDPR consent)
- JUVE / Chambers rankings (manual entry — no API available)
- **BLOCKER**: CV Mirroring DE → weil.com (EN). English CVs must be automatically pushed to the main site's People section. Requires Sitecore API access. Phase 1 workaround: manual CSV export.
- **BLOCKER**: Track Record sync with press releases

### 3. EXPERTISE / SERVICES
- 7 Practice Areas: M&A/PE, Litigation/Arbitration, Banking & Finance, Regulatory/Compliance, Restructuring/Insolvency, Tax, Employment
- Implemented as **tab-based layout** (not separate landing pages)
- Insights dynamically linked to Partners (three-way relation: Person ↔ Practice ↔ Insight)

### 4. NEWS & INSIGHTS
- Local press releases (standard WordPress posts)
- Insights / Thought Leadership (CPT with category taxonomy: News, Insight, Press Release)
- Filter and search functionality
- **BLOCKER**: Optional US Newsroom sync via Sitecore API (Phase 2)

### 5. CAREERS / HR HUB
- Life at Weil Germany — testimonials
- Benefits section (static)
- **BLOCKER**: Open Positions — unknown ATS landscape (Workday? Greenhouse? SAP SF? Manual?). Phase 1: WordPress CPT with manual job management.
- **BLOCKER**: Application Form — simple form with GDPR consent in Phase 1, full ATS flow in Phase 2.
- GDPR: Datenschutzerklaerung confirmation via email (opt-in link after submission), data retention max 6 months

### 6. MULTILINGUAL (DE/EN)
- WPML plugin for all CPTs, taxonomies, ACF fields
- DE/EN toggle in header, hreflang tags, canonical URLs
- **BLOCKER**: Content translation effort for 50+ profiles, all pages — who translates? (internal / agency / machine translation)

### 7. TECHNICAL REQUIREMENTS
- **BLOCKER**: GDPR applicant data protection — retention periods, deletion concept, DPA with WPEngine (US hosting!)
- Cookie consent management (granular DE/EU consent required)
- Video: native player + lazy loading, 2-click GDPR consent
- Imprint + Privacy Policy (must be provided by Weil legal)
- Mobile-First + Core Web Vitals optimization
- Instant-Editing: custom theme development based on client spec (Gutenberg)

### 8. INFRASTRUCTURE
- **BLOCKER**: Sitecore API Access — required for CV mirroring and News sync. Version, auth, endpoints all unknown.
- **BLOCKER**: WPEngine access — admin level, SFTP/SSH, staging needed. Plugin restrictions unknown.
- Deployment workflow: Git-based preferred, staging → production

## Critical Decisions (Unresolved)

These must be resolved in the Requirements Workshop before binding cost estimate:

1. **ATS System**: Does Weil have an existing Applicant Tracking System? Which one? Can de.weil.com integrate or should it redirect?
2. **Sitecore API**: Version? GraphQL/REST? Who is the US technical contact?
3. **Translation**: Internal team, agency, or machine translation for DE/EN content?
4. **CV Mirroring**: Data format, required fields, sync frequency?
5. **Applicant Data**: Where stored, how confirmed (Datenschutzerklaerung email flow), DPA with WPEngine?

## Phased Approach

### Phase 1 — Standalone (Target: April 2026)
WordPress without external integrations. All content managed manually by DE team. Zero dependency on US IT. This is the go-live scope.

### Phase 2 — Integration (From May 2026)
- Sitecore API: CV mirroring (DE → EN on weil.com)
- Sitecore API: US Newsroom article sync
- ATS integration (if system is identified)
- Advanced features based on workshop outcomes

## Preliminary Roadmap

| Phase | Weeks | Milestone |
|-------|-------|-----------|
| Requirements Workshop | W1-2 | Resolve blockers, define scope |
| Design & Architecture | W3-4 | Theme concept, data model, infrastructure setup |
| Core Development | W5-8 | Custom theme, CPTs, profiles, practices, news |
| Content & Translation | W9-10 | Content entry, DE/EN translation, QA |
| Testing & Go-Live | W11-12 | UAT, performance, SEO audit, launch |
| Phase 2: Integration | W13+ | Sitecore API, ATS, advanced features |

## Data Model (WordPress)

### Custom Post Types
- `attorney` — profiles with ACF fields (photo, bio, practices, education, bar admissions, publications, awards, video)
- `insight` — articles/updates linked to attorneys and practices
- `deal` — deal highlights / selected references
- `position` — open job listings (Phase 1: manual; Phase 2: ATS sync)
- `testimonial` — Life at Weil employee stories

### Taxonomies
- `practice-area` — 7 practice areas (shared across attorneys, insights, deals)
- `insight-type` — News, Insight, Press Release
- `office` — Frankfurt (+ future offices)
- `title` — Partner, Counsel, Associate

### Key Relationships (ACF)
- Insight → Attorney (relationship field)
- Insight → Practice Area (taxonomy)
- Attorney → Practice Area (taxonomy)
- Deal → Practice Area (taxonomy)
- Deal → Attorney (relationship field)

## Brand & Design

- **Main site**: weil.com — dark, authoritative, premium legal aesthetic
- **Brand color**: Weil Green `#43a047`
- **Typography**: Must align with global brand standards
- **Design principle**: Clean, professional, editorial feel — not generic corporate WordPress
- **Mobile-first**: Core Web Vitals compliance mandatory

## GDPR Requirements (Critical for DE)

- Cookie consent: granular (Marketing, Analytics, Functional) — Borlabs/Cookiebot/Complianz
- Video embeds: 2-click consent (facade pattern for Vimeo/YouTube)
- Imprint (Impressum): legally required, provided by Weil legal
- Privacy Policy (Datenschutzerklaerung): separate from US version
- Applicant data: max 6 months retention, automated deletion, confirmation email with opt-in
- DPA (Data Processing Agreement) with WPEngine required (US hosting)

## Key Files in This Repo

- `CLAUDE.md` — this file
- `docs/briefing.pdf` — original client briefing (German, 3 pages)
- `docs/weil-dashboard.jsx` — interactive requirements analysis dashboard (React)
- `wp-content/themes/weil-de/` — custom WordPress theme (to be created)

## Development Guidelines

- PHP 8.2+, WordPress 6.x
- Follow WordPress Coding Standards
- Use ACF Pro for all custom fields (do not hardcode meta)
- WPML-compatible from day one (all strings translatable)
- Git-based workflow: `main` → `staging` → `production`
- No page builders (Elementor, Divi, etc.) — Gutenberg + custom blocks only
- Performance budget: LCP < 2.5s, CLS < 0.1, FID < 100ms

## Contact & Access (To Be Confirmed)

- **Client**: Dr. Sepita Ansari (Weil Frankfurt)
- **US IT Contact**: TBD (needed for Sitecore API, WPEngine, DNS)
- **WPEngine**: Access level TBD
- **Sitecore**: Version and API access TBD
