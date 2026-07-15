# Seeded Accessibility Issues — Discover Saturn / Halo Estates fixture

This site is an **intentionally-inaccessible WCAG training fixture**. The accessibility
problems below were introduced on purpose. **Do not fix them** — they are the reason the
fixture exists.

This catalog was produced by auditing the HTML source directly (page by page), independent
of any scanner. It is meant to be compared against the AAArdvark scan results to see which
seeded issues an automated scan catches versus which require manual review.

- **Audit date:** 2026-07-14
- **Method:** Manual source review of all 9 HTML pages
- **Pages:** index, results, property-detail, compare, about, advisors, contact, privacy, terms

**Legend**
- **Detectable** — likely caught by an automated (axe-core–style) scanner
- **Partial** — a scanner may flag it, often as "needs review," or catches only part of it
- **Manual** — requires human review; automated scanners generally miss it
- **Tagged** — element carries an explicit `data-a11y-issue="..."` marker in the source

---

## A. Site-wide issues (shared header / footer / `<head>` chrome)

These appear on **every page** because they live in the shared chrome. In the seed catalog
they are numbered #2, #4, #6, #12.

| ID | Issue | WCAG SC | Level | Detectable | Tagged |
|----|-------|---------|-------|------------|--------|
| #4 | `<html>` missing `lang` attribute | 3.1.1 Language of Page | A | **Detectable** | — |
| #6 | Generic, non-descriptive `<title>Halo Estates</title>` (same on every page) | 2.4.2 Page Titled | A | Manual | — |
| #12 | Focus outline removed site-wide: `*:focus{ outline:none !important; }` | 2.4.7 Focus Visible | AA | Partial | — |
| #2 | Header search input has placeholder only, no label / no accessible name | 3.3.2 + 4.1.2 | A | **Detectable** | `unlabeled-search-input` |

**Additional latent issues also present in the shared chrome** (not part of the numbered
seed catalog, but real and present on every page):

| Issue | WCAG SC | Level | Detectable |
|-------|---------|-------|------------|
| No "skip to main content" link | 2.4.1 Bypass Blocks | A | Partial |
| "Sign In" link points to `href="#"` (dead destination) | 2.4.4 Link Purpose | A | Manual |
| Low-contrast gold text `#b0823f` on paper `#f7f3ec` (~3.1:1) | 1.4.3 Contrast (Minimum) | AA | Detectable |
| Low-contrast muted text `#6c7280` on paper `#f7f3ec` (~4.4:1) | 1.4.3 Contrast (Minimum) | AA | Detectable |
| Footer copyright `#6c7488` on ink `#0e1526` (~4.0:1) | 1.4.3 Contrast (Minimum) | AA | Detectable |
| Breadcrumb not marked up as `<nav>`/list; literal `»` read aloud | 1.3.1 Info & Relationships | A | Manual |
| Footer link groups are `<div>` stacks, not lists/`<nav>` | 1.3.1 Info & Relationships | A | Manual |

> Note: The four static "content" pages (**about, advisors, contact, privacy, terms**) seed
> **no new body-level catalogued issues** — their only numbered seeds are the shared-chrome
> four (#2/#4/#6/#12). The contrast, skip-link, and breadcrumb items above are the latent
> extras that ride along in the chrome. The interactive pages (**index, results,
> property-detail, compare**) seed additional body issues, listed below.

---

## B. Numbered seed catalog (issue slugs)

The interactive pages tag elements with `data-a11y-issue="<slug>"`. Consolidated list:

| # | Slug / description | WCAG SC | Level | Pages |
|---|--------------------|---------|-------|-------|
| #1 | `*-image-no-alt` — informative image missing `alt` | 1.1.1 | A | index, results, property-detail, compare, about |
| #2 | `unlabeled-search-input` — header search, placeholder only | 3.3.2 / 4.1.2 | A | all |
| #3 | `low-contrast-*` — pale text below 4.5:1 | 1.4.3 | AA | index, results, property-detail, about |
| #4 | missing `lang` | 3.1.1 | A | all |
| #5 | icon-only control, `role=button`, no accessible name | 4.1.2 | A | index, results, property-detail, compare, about |
| #6 | generic `<title>` | 2.4.2 | A | all |
| #7 | `heading-skip-h1-to-h3` — heading level skipped | 1.3.1 | A | index, results, property-detail, about |
| #8 | `identical-*-links` — repeated link text, no context | 2.4.4 | A | index, results, property-detail, compare, about |
| #9 | `unlabeled-price` — min/max number inputs, no label | 3.3.2 / 4.1.2 | A | results |
| #11 | newsletter error: color-only + not associated with field | 1.4.1 / 3.3.1 | A | index |
| #12 | focus outline removed | 2.4.7 | AA | all |
| #13 | `*-no-alt-judgment` — hero image missing `alt` (judgment case) | 1.1.1 | A | index, property-detail, about |
| #15 | `unlabeled-*` `<select>` — beds / sort, no accessible name | 3.3.2 / 4.1.2 | A | results, compare |

*(No #10 or #14 slug was found in the source.)*

---

## C. Per-page detail

### index.html (Home)

| Issue | WCAG SC | Level | Count / location | Detectable | Tagged |
|-------|---------|-------|------------------|------------|--------|
| Images missing `alt` | 1.1.1 | A | 10 (1 hero #13 + 6 cards + 2 neighborhood + 1 lifestyle) | **Detectable** | `*-no-alt`, `hero-image-no-alt-judgment` |
| Heading skip H1→H3 (no H2 anywhere) | 1.3.1 | A | line ~102 | **Detectable** | `heading-skip-h1-to-h3` |
| Low-contrast hero sub-copy `#d8c39a` over photo | 1.4.3 | AA | line ~74 | Partial (text over image) | `low-contrast-hero-subcopy` |
| Newsletter error: color-only, not associated, not announced | 1.4.1 / 3.3.1 / 4.1.3 | A/AA | lines ~281–285 | Manual | `newsletter-error-color-only-unassociated` |
| Icon-only `role=button` controls, no name | 4.1.2 | A | 7 (1 hero search submit #5 + 6 favorite hearts) | **Detectable** | `hero-search-submit-no-name`, `favorite-toggle-no-name` |
| `role=button` divs not keyboard-operable (no `tabindex`/keys) | 2.1.1 | A | 10 (submit + 3 filter chips + 6 favorites) | Partial | — |
| Hero "Where" + newsletter inputs: placeholder-only, no label | 3.3.2 / 4.1.2 | A | 2 (+ header search) | **Detectable** | — |
| Identical "Explore" links, same text + destination | 2.4.4 | A | 6 | Partial | `identical-explore-links` |

### results.html (All residences)

| Issue | WCAG SC | Level | Count / location | Detectable | Tagged |
|-------|---------|-------|------------------|------------|--------|
| Result-card images missing `alt` | 1.1.1 | A | 8 | **Detectable** | `result-card-image-no-alt` |
| Heading skip H1→H3 (→H4; no H2) | 1.3.1 | A | line ~82 | **Detectable** | `heading-skip-h1-to-h3` |
| Low-contrast result count `#c3b89f` on paper (~1.6:1) | 1.4.3 | AA | line ~146 | **Detectable** | `low-contrast-count` |
| Price min/max number inputs, no label | 3.3.2 / 4.1.2 | A | 2 | **Detectable** | `unlabeled-price` |
| Bedrooms `<select>` + Sort `<select>`, no accessible name | 3.3.2 / 4.1.2 | A | 2 | **Detectable** | `unlabeled-bedrooms`, `unlabeled-sort` |
| Icon-only `role=button` controls, no name | 4.1.2 | A | 10 (2 view toggles #5 + 8 favorites) | **Detectable** | `favorite-toggle-no-name` |
| `role=button` divs not keyboard-operable | 2.1.1 | A | ~14 (reset, cat filters, view toggles, favorites, empty-reset) | Partial | — |
| Custom checkboxes expose `role=button`, no `aria-checked` state | 4.1.2 | A | 3 (category rows, "full ring view only") | Manual | — |
| Identical "View details" links | 2.4.4 | A | 8 | Partial | `identical-view-details` |

### property-detail.html (Aurelia)

| Issue | WCAG SC | Level | Count / location | Detectable | Tagged |
|-------|---------|-------|------------------|------------|--------|
| Images missing `alt` | 1.1.1 | A | 11 (1 hero + 5 thumbs + 1 interior + 3 similar cards + 1 lightbox) | **Detectable** | — |
| Map image with meaningless `alt="map.png"` | 1.1.1 | A | line ~241 | Manual | — |
| Heading skip H1→H3 (→H4; no H2) | 1.3.1 | A | line ~153 | **Detectable** | — |
| Low-contrast facts strip: label `#586178` on ink `#0e1526` | 1.4.3 | AA | lines ~139–146 | **Detectable** | `low-contrast-facts-strip` |
| **Lightbox is a keyboard trap** (swallows Tab + Esc; mouse-only) | 2.1.2 (+2.1.1/2.4.3) | A | lines ~321–383 | Manual | — |
| Form validation errors color-only + not associated | 1.4.1 / 3.3.1 | A | lines ~212–226, 419–423 | Manual | — |
| Icon-only `role=button` controls, no name | 4.1.2 | A | 8 (gallery prev/next, favorite, share, map pin, lightbox close/prev/next) | **Detectable** | — |
| `role=button`/clickable elements not keyboard-operable | 2.1.1 | A | 11 | Partial | — |
| Unlabeled form controls (placeholder-only or fully unlabeled) | 3.3.2 / 4.1.2 | A | 9 (search + 4 calculator + 4 viewing-form; `#fDate` fully unlabeled) | **Detectable** | — |
| Required fields not marked (`required`/visible indicator) | 3.3.2 | A | name/email/date | Manual | — |
| Identical "View details" links | 2.4.4 | A | 3 | Partial | — |

### compare.html (Compare residences)

| Issue | WCAG SC | Level | Count / location | Detectable | Tagged |
|-------|---------|-------|------------------|------------|--------|
| Comparison images missing `alt` | 1.1.1 | A | 3 (static + regenerated by JS) | **Detectable** | `compare-image-no-alt` |
| Comparison `<table>` has no `<th>`/`scope`/`<caption>` — all `<td>` | 1.3.1 | A | lines ~97–186 | **Detectable** | `comparison-table-no-header-semantics` |
| Remove-column icon buttons, `role=button`, no name | 4.1.2 | A | 3 | **Detectable** | (in `data-remove` divs) |
| Remove-column + add-residence `role=button` divs not keyboard-operable | 2.1.1 | A | 5 | Partial | — |
| Sort `<select>`, no accessible name | 3.3.2 / 4.1.2 | A | line ~83 | **Detectable** | `unlabeled-sort` (#15) |
| Identical "View" links (3, same destination) | 2.4.4 | A | 3 | Manual | — |
| Low-contrast gold/muted/footer text | 1.4.3 | AA | multiple | **Detectable** | — |

### about.html

| Issue | WCAG SC | Level | Count / location | Detectable | Tagged |
|-------|---------|-------|------------------|------------|--------|
| Images missing `alt` | 1.1.1 | A | 3 (hero #13 + story + CTA background) | **Detectable** | `*-no-alt`, judgment |
| Heading skip H1→H3 (no H2) | 1.3.1 | A | line ~81 | **Detectable** | `heading-skip-h1-to-h3` |
| Low-contrast stat band: label `#586178` on ink (~2.95:1) | 1.4.3 | AA | lines ~122–126 | **Detectable** | `low-contrast-stat-band` |
| Icon-only contact buttons (mail/call), `role=button`, no name | 4.1.2 | A | 6 | **Detectable** | (icon buttons #5) |
| Those same buttons not keyboard-operable | 2.1.1 | A | 6 | Manual | — |
| Identical "Get in touch" links (3 advisors, same text/href) | 2.4.4 | A | 3 | Manual | `identical-get-in-touch-links` |
| "By the Numbers" stat band not semantically structured | 1.3.1 | A | lines ~122–126 | Manual | — |
| + shared-chrome four (#2/#4/#6/#12) | — | — | — | — | — |

### advisors.html · contact.html · privacy.html · terms.html

These pages seed **only the shared-chrome four** (#2 search, #4 lang, #6 title, #12 focus)
plus the latent chrome extras from Section A (contrast, no skip link, `href="#"` Sign In,
non-semantic breadcrumb/footer). Page-specific notes:

- **contact.html** — has a contact form, but per the source it seeds **no new labelled-form
  issue**; the form controls' state depends on the shared chrome. (Worth a closer manual look
  if you expect form-label seeds here — none were tagged.)
- **advisors.html** — advisor "avatars" are text initials, not images, so no alt issues; clean
  heading order (H1→H2→H3).
- **privacy.html / terms.html** — no `<img>` elements; clean heading order (single H1 → H2s).

---

## D. Summary counts (seeded + confirmed latent)

| WCAG SC | Level | Approx. instances across site |
|---------|-------|-------------------------------|
| 1.1.1 Non-text Content (missing/bad alt) | A | ~35 images (index 10, results 8, property 12, compare 3, about 3) |
| 1.3.1 Info & Relationships (heading skip, table headers, structure) | A | 4 heading-skips + 1 headerless table + structural |
| 1.4.1 Use of Color (color-only errors) | A | 2 (index, property-detail forms) |
| 1.4.3 Contrast (Minimum) | AA | Seeded on 4 pages + site-wide gold/muted/footer |
| 2.1.1 Keyboard (inoperable role=button divs) | A | ~40+ controls across interactive pages |
| 2.1.2 No Keyboard Trap (lightbox) | A | 1 (property-detail) |
| 2.4.1 Bypass Blocks (no skip link) | A | all 9 pages |
| 2.4.2 Page Titled (generic title) | A | all 9 pages |
| 2.4.4 Link Purpose (identical links, `href="#"`) | A | index 6, results 8, property 3, compare 3, about 3 |
| 2.4.7 Focus Visible (outline removed) | AA | all 9 pages |
| 3.1.1 Language of Page (no lang) | A | all 9 pages |
| 3.3.1 Error Identification | A | 2 (index, property-detail) |
| 3.3.2 Labels or Instructions (unlabeled inputs/selects) | A | header search ×9 + price ×2 + selects ×3 + calculator/form ×8 |
| 4.1.2 Name, Role, Value (icon buttons, unnamed selects) | A | ~30+ controls |

---

## E. How this maps to an automated scan (expectation)

An axe-core–style scanner should reliably catch the **Detectable** rows: missing `alt`,
missing `lang`, missing form labels / select names, empty-name `role=button` controls, heading
order, headerless data table, and solid-background contrast failures.

It will likely **miss or only partially flag** the **Manual/Partial** rows: generic title,
removed focus outline, missing skip link, keyboard operability of `role=button` divs, the
lightbox keyboard trap, color-only/unassociated form errors, identical-link ambiguity,
required-field marking, and text-over-image contrast.

Use Section C's "Detectable" column as the predicted overlap when comparing against the
AAArdvark scan results.
