# Lessons

Problems that cost time and the fixes that worked. Unlike decisions, lessons
are never archived or pruned: the answer you need months later is exactly the
one nobody remembers. Add a new entry at the top. Edit an old one only to
correct it or to note a case where it didn't hold.

Search here before solving a problem that feels familiar:
`./scripts/search.sh <one distinctive word>`

<!--
Entry template:

## <Short title naming the symptom>
- **Problem:** <what went wrong, and how it showed up>
- **Fix:** <what worked>
- **Doesn't apply when:** <the case where following this would be a mistake>
-->


## Blank page before major heading after a section break
- **Problem:** A major heading (e.g. APPENDICES, APPENDIX B, METHODOLOGY) opened on a page with a large empty gap, or sat alone after a fully blank page. PDF showed 1-word or empty pages before the heading.
- **Root cause:** The heading had `w:pageBreakBefore=true` *and* followed a section break (`w:sectPr` on the previous paragraph). Word/LibreOffice treat each as a page break: the section break creates page N; `pageBreakBefore` creates page N+1; page N is left blank. Leading empty paragraphs after the section break made the gap worse.
- **Fix:**
  1. If a major heading follows a section break, **do not** set `pageBreakBefore` — the section break already starts the new page.
  2. Use `pageBreakBefore` only when there is **no** preceding section break and you still need a new page.
  3. Remove consecutive empty body paragraphs that sit between a section break and the next heading.
  4. Treat section/page breaks as counting for ~1 spacing unit so you do not also stack large `before` spacing on top of the break.
- **Doesn't apply when:** The heading does not follow a section break (then `pageBreakBefore` is the right tool for "always start major headings on a new page"). Also does not apply to intentional blank pages (none in this thesis).

## Major heading “3-after” spacing not visible
- **Problem:** XML showed `before=360/720` and `after=360/720` on major headings, but the PDF still looked like only ~1 blank line after INTRODUCTION, METHODOLOGY, etc.
- **Root cause:** `w:keepNext` was set on major chapter headings. Word/LibreOffice keep the heading with the following paragraph and **collapse or hide the after-spacing**, so the gap never shows.
- **Fix:** Turn **`keepNext` OFF** on chapter majors (INTRODUCTION, METHODOLOGY, RESULTS…, CONCLUSIONS AND RECOMMENDATIONS, REFERENCES). Keep `keepNext` for minors/captions where orphan control matters. Use a consistent unit scale (here: 1 space = 240 twips, 3 spaces = 720).
- **Doesn't apply when:** You intentionally want a heading glued to the next line (e.g. caption above a table); then `keepNext` is correct and you accept little/no after-gap.

## Minor “1-before” looked the same as major “3”
- **Problem:** Minors and majors appeared to have the same gap length even when XML differed.
- **Root cause:** Inconsistent units (minor before=120 while major=720), plus the old rule “after a major, zero the minor’s before so only major after counts,” which erased the minor’s own 1-space.
- **Fix:** Use one scale: **1 = 240 twips, 3 = 720**. Minors: `before=240`, `after=0`. Majors: `before=720`, `after=720` (with `keepNext` off). Do not zero minor before just because a major precedes it unless the user explicitly wants only the major’s after-gap.
- **Doesn't apply when:** User specifies a different visual scale (e.g. appendix majors at 1-space so Quick-Reference fits one page).

## Table caption splits from table body (LibreOffice PDF)
- **Problem:** “Table N” sat alone at the bottom of a page; table body started on the next page. `keepNext` on the caption did not help in LibreOffice export.
- **Root cause:** LibreOffice often **ignores `keepNext` across a paragraph → table** boundary. `pageBreakBefore` on the caption alone can still leave a orphan caption if the table doesn’t fit.
- **Fix:** Prefer **external** captions (paragraph above the table), not labels embedded in the first header cell (embedding broke column layout). Accept that LO may still split caption/table sometimes; avoid putting the label *inside* the table. Use smaller table font/single cell line-spacing so tables fit more often on the same page as the caption.
- **Doesn't apply when:** Exporting only with Microsoft Word (keepNext p→tbl is more reliable there).

## Do not embed table labels inside header cells
- **Problem:** Putting “Table 1: Title | Category” into the first header cell fixed caption orphans but **messed up the whole table** (wrong first-column text, layout).
- **Fix:** Keep **Table N + title as normal paragraphs above the table**. Restore pure column headers in the first row.
- **Doesn't apply when:** A template deliberately uses a single-row title band as part of the table design (not this thesis).

## Title page: double spacing pushes name/date to page 2
- **Problem:** With body double spacing (line=480) and the full empty-line structure, name and date overflowed to page 2.
- **Fix:** Title page only: use **1.5 line spacing** (`line=360`). Tune empties before the name (about **5** at 1.5) so name + date stay on page 1 at the bottom. Body stays double. Section break after the date; INTRODUCTION at top of page 2 with `before=0`.
- **Doesn't apply when:** Institution requires double spacing on the title page and allows a two-page title block.

## OOXML `pPr` child order / invalid elements fail pack
- **Problem:** `pack.py` validation failed (e.g. `wordWrap` “element is not expected”); docx did not update; PDF still showed old formatting.
- **Root cause:** `w:pPr` children must follow the schema order; inserting elements in the wrong order or unsupported positions fails validation.
- **Fix:** After editing `pPr`, **reorder children** to the known sequence (keepNext → pageBreakBefore → spacing → jc → … → sectPr). Prefer not adding optional elements (like `wordWrap`) unless required and ordered correctly. Always confirm pack validation PASSED before trusting the PDF.
- **Doesn't apply when:** Editing only run-level `rPr` (fonts/sizes) with no `pPr` changes.

## Trailing blank page at end of document
- **Problem:** PDF ended with an empty (or near-empty) final page after the last real content (e.g. after Appendix C).
- **Root cause:** Not the same as the mid-doc “heading after section break” bug. An **extra** section break and/or empty paragraphs sat **after the last content**, so Word/LibreOffice emitted one more page. A single body-level `w:sectPr` at the end of `w:body` is normal and required; a *second* section boundary or leftover empties after content is what creates the trailing blank.
- **Fix:**
  1. Remove empty paragraphs after the last content paragraph.
  2. Remove any redundant trailing section break so only the standard final body `sectPr` remains.
  3. Re-export PDF and confirm the last page still has text.
- **Doesn't apply when:** You intentionally want a blank back page. Also different from mid-document blanks caused by `pageBreakBefore` + section break before a major heading (see that lesson).

