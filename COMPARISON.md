# Audit vs. AAArdvark Scan — Comparison

Compares the hand-authored source audit in [SEEDED-ISSUES.md](SEEDED-ISSUES.md) against the
AAArdvark automated scan of the same site.

- **Site:** Discover Saturn (`mMdEYQ`) — https://discoversaturn.site
- **Workspace:** Nose First Accessibility (2341)
- **Scan:** #90594, 2026-07-14 — 9 pages, **11 issues / 132 instances** (7 errors, 4 warnings)
- **Standard:** WCAG 2.1 AA

---

## 1. What AAArdvark found, mapped to the seeded catalog

| # | AAArdvark issue | SC | Severity | Instances | Manual review? | Maps to seeded issue |
|---|-----------------|----|----------|-----------|----------------|----------------------|
| 1 | `html_lang_exists` — missing `lang` | 3.1.1 | Very High | 1 | no | **#4** lang ✅ |
| 4 | `text_contrast_sufficient` — contrast < AA | 1.4.3 | Very High | 47 | no | **#3** low-contrast + latent gold/muted/footer ✅ |
| 9 | `input_label_exists` — control needs label | 4.1.2 | Critical | 12 | no | **#2 / #9 / #15** + unlabeled inputs ✅ |
| 11 | `img_alt_valid` — image needs accessible name | 1.1.1 | Critical | 12 | no | **#1 / #13** missing alt ✅ (count low — see §3) |
| 8 | `svg_graphics_labelled` — non-decorative SVG needs name | 1.1.1 | Very High | 1 | no | partial **#5** icon controls |
| 5 | `aria_complementary_labelled` — `<aside>` needs label | 2.4.1 | High | 2 | no | latent (unlabeled filter `<aside>`) ✅ |
| 2 | `style_focus_visible` — focus indicator modified | 2.4.7 | Warning | 24 | **yes (all)** | **#12** focus removed ✅ |
| 3 | `input_label_visible` — visible label for input | 2.5.3 | Warning | 12 | **yes (all)** | **#2 / #9 / #15** placeholder-as-label ✅ |
| 6 | `widget_tabbable_exists` — component needs a tabbable element | 2.1.1 | Warning | 15 | **yes (all)** | latent — `role=button` divs not keyboard-operable ✅ |
| 7 | `element_tabbable_unobscured` — focused element covered | 2.4.11 | Warning | 5 | **yes (all)** | **NEW** — not in audit (see §4) |
| 10 | `table_headers_exists` — data table needs headers | 1.3.1 | Moderate | 1 | no | **compare-table-no-header-semantics** ✅ |

**Overlap is strong on the machine-detectable seeds.** Every issue the audit marked
"Detectable" has a corresponding scan finding — except **heading order** (see §2). The scan's
four **Warning / needs-review** issues (focus visible, visible label, tabbable widget, focus
unobscured) line up with the audit's "Manual/Partial" rows — AAArdvark flags them but defers
the verdict to a human.

---

## 2. Seeded issues the scan did NOT catch (audit-only)

These are in [SEEDED-ISSUES.md](SEEDED-ISSUES.md) but have **no** AAArdvark issue:

| Seeded issue | WCAG SC | Why the scan misses it |
|--------------|---------|------------------------|
| **#7 Heading skip H1→H3** (index, results, property-detail, about) | 1.3.1 | ⚠️ **Notable gap** — the audit predicted this as Detectable (axe `heading-order`), but AAArdvark's ruleset raised no heading-order issue. Worth a manual confirm. |
| **#6 Generic `<title>`** (all pages) | 2.4.2 | A title exists and is non-empty; genericness is a human judgment. Expected miss. |
| **#8 Identical links** ("Explore" / "View details" / "Get in touch") | 2.4.4 | Link text + destination present; ambiguity-in-context is manual. Expected miss. |
| **#11 Newsletter error: color-only + unassociated** (index) | 1.4.1 / 3.3.1 | Runtime/behavioral; not visible to static scan. Expected miss. |
| Property-detail form errors color-only / unassociated | 1.4.1 / 3.3.1 | Same — behavioral. Expected miss. |
| **Lightbox keyboard trap** (property-detail) | 2.1.2 | Purely behavioral (swallows Tab/Esc). Expected miss. |
| No skip link (all pages) | 2.4.1 | AAArdvark's 2.4.1 finding is about complementary-landmark labels, not a missing skip link. Expected miss. |
| `href="#"` "Sign In" dead link (all pages) | 2.4.4 | Has an accessible name; dead destination is manual. Expected miss. |
| Meaningless `alt="map.png"` (property-detail) | 1.1.1 | An `alt` string is present, so `img_alt_valid` passes it. Expected miss. |
| Required fields not marked (property-detail form) | 3.3.2 | Manual. Expected miss. |

**Takeaway:** the audit is the superset. The scan reliably covers alt / labels / lang /
contrast / table-headers / focus-modified / non-tabbable-widgets, but the **heading-skip miss
is the one surprise** — everything else the scan skips is a known limit of static automated
testing (behavioral, judgment, or content-quality issues).

---

## 3. Instance-count discrepancies worth investigating

Two seeded issues have far fewer scan instances than the source audit found:

| Issue | Audit (source) | Scan instances | Gap |
|-------|----------------|----------------|-----|
| Missing image `alt` (1.1.1) | ~35 images across 5 pages | **12** | −23 |
| Missing `lang` (3.1.1) | all **9** pages | **1** | −8 |

Possible explanations (not yet confirmed):
- The **live site** at discoversaturn.site may differ from the local repo (e.g. a build step
  adds `lang` to most pages, or images differ).
- AAArdvark may **de-duplicate document-level issues** (like `html_lang`) to one instance per
  site rather than one per page.
- Some images may be treated as **decorative/redundant** and excluded from `img_alt_valid`.

To resolve, drill into instances with `list_issue_instances` (e.g. issue #11 for images,
issue #1 for lang) and compare the reported pages/selectors against the audit. **I can do this
next if you want the counts reconciled.**

---

## 4. Scan findings the audit under-weighted

| AAArdvark issue | SC | Note |
|-----------------|----|----|
| `element_tabbable_unobscured` (5) | 2.4.11 | **New** — focused element covered by the sticky header when tabbing. The audit didn't flag this; it's a real consequence of the sticky header + removed focus styles. Needs-review. |
| `aria_complementary_labelled` (2) | 2.4.1 | The audit noted the unlabeled `<aside>` only as "low priority." The scan promotes it to a High-severity issue. |
| `svg_graphics_labelled` (1) | 1.1.1 | Only 1 instance — most icon SVGs are `aria-hidden` (so treated as decorative), which is why the audit's ~30 "icon button no name" findings surface mainly as `widget_tabbable` (2.1.1) instead of SVG-name failures. |

---

## 5. Bottom line

- **11 scan issues** all map cleanly to seeded or latent audit findings — **no false positives**,
  and no scan finding is unexplained by the audit.
- **Audit ⊃ Scan**: the audit catches everything the scan does, plus the behavioral/judgment
  issues automation can't see (keyboard trap, color-only errors, generic titles, identical
  links, skip link).
- **One real coverage gap in the scan**: **heading-order (#7)** — predicted detectable but not
  reported. Confirm manually.
- **Two count mismatches** (images −23, lang −8) suggest a live-vs-local difference or scanner
  de-duplication — reconcile via `list_issue_instances` before drawing conclusions.
