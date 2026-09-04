# `demos/` — Circle mastermind teaching pages

**These pages are not part of the Discover Saturn fixture.** Read that sentence twice before
changing anything in here, because the rule that governs the rest of this repository is inverted
in this directory.

- The **fixture** (the nine HTML pages at the site root) is *intentionally inaccessible*. Its
  seeded WCAG failures are catalogued in [`../SEEDED-ISSUES.md`](../SEEDED-ISSUES.md) and must not
  be fixed.
- The pages in **`demos/`** are *intentionally clean*, apart from the single control or single
  structure each one exists to demonstrate. That isolation is the whole point: a live scan of a
  demo page should surface the teaching point and nothing else.

Built for the AAArdvark Circle mastermind on 4 September 2026, "Semantic HTML: What to Ask For and
How to Check It". Deck and outline live in the operations workspace under `.working/circle/`.

## The pages

| Page | Deck slide | What it demonstrates | Expected scan result |
|---|---|---|---|
| `index.html` | — | Hub linking the five demos | Clean |
| `controls.html` | 6 | Native `button` vs link-styled-as-button vs `div[role=button][tabindex=0]`, all identical on screen | **Clean.** All three controls have a role, a name and focus. Only behaviour separates them. |
| `headings.html` | 11 | Obvious visual hierarchy, scrambled heading levels (h1, h6, h5, h3, h2, h6, h4, h3) | **Flags heading order / 1.3.1.** That is intended. |
| `tables.html` | 16 | Same data as a layout table and as a real table with `caption` + `scope` | **Flags the layout table** (missing header semantics). The second table is correct. |
| `heart-before.html` | 18 | The homepage save toggle exactly as shipped | **Exactly one finding:** `role="button"` with no accessible name (4.1.2, A). |
| `heart-after.html` | 19–20 | The same toggle with `aria-label` + `tabindex` added and the click-only handler untouched | **Clean.** It still fails 2.1.1 and 1.4.1 in practice. That gap is the slide. |

## Conventions

- **Not in `sitemap.xml`, not in the site navigation.** They are reachable only by direct link, and
  from `demos/index.html`. Keep it that way, so fixture scan counts stay comparable to
  `SEEDED-ISSUES.md`.
- **Contrast-verified palette.** `--gold` is `#7f5a1c` here, not the fixture's `#b0823f` (3.11:1,
  a seeded 1.4.3 failure), and `--muted` is `#5c6272`, not `#6c7280` (4.36:1). If you add colours,
  check them before committing or the "green scan" demo stops working.
- **No heading elements outside the specimen on `headings.html`.** Every panel label there is a
  styled paragraph, so a heading-map extension or `Insert+F7` run on that page returns exactly the
  specimen outline with no demo-tool noise.
- **Observation-only listeners.** Where a page counts keypresses on a broken control, the listener
  records and never activates. The broken control stays broken.
- Images are referenced as `../saturn/images/…`.

## Regenerating

These are hand-committed static HTML, matching the rest of the repository. They were generated once
from a throwaway builder script; there is no build step here and none should be added. Edit the HTML
directly.
