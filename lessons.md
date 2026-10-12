# Lessons

Problems that cost time and the fixes that worked. Unlike decisions, lessons
are never archived or pruned: the answer you need months later is exactly the
one nobody remembers. Edit an old entry only to correct it or to note a case
where it didn't hold.

Search here before solving a problem that feels familiar:
`./scripts/search.sh <one distinctive word>`

## Organization rules (lookup & recording)

1. **Umbrella first, alphabetically.** Group entries under a short major-bug
   name (e.g. Blank pages, Spacing, Tables). Sort those umbrella headings A–Z.
2. **Related bugs together under the same umbrella.** When recording a new
   lesson, put it under an existing umbrella if it is the same kind of failure;
   only invent a new umbrella when nothing fits.
3. **Within an umbrella,** keep a stable order (oldest-first or symptom name
   A–Z—pick one and stay consistent). Prefer symptom names that a future
   search will hit.
4. **Do not** dump unrelated one-off notes at the top; always file under an
   umbrella so the next session can scan headings fast.

<!--
Entry template (nest under an ## Umbrella heading):

### <Short title naming the symptom>
- **Problem:** <what went wrong, and how it showed up>
- **Fix:** <what worked>
- **Doesn't apply when:** <the case where following this would be a mistake>
-->

## Blank pages

### Blank page before major heading after a section break
- **Problem:** A major heading (e.g. APPENDICES, APPENDIX B, METHODOLOGY) opened on a page with a large empty gap, or sat alone after a fully blank page. PDF showed 1-word or empty pages before the heading.
- **Root cause:** The heading had `w:pageBreakBefore=true` *and* followed a section break (`w:sectPr` on the previous paragraph). Word/LibreOffice treat each as a page break: the section break creates page N; `pageBreakBefore` creates page N+1; page N is left blank. Leading empty paragraphs after the section break made the gap worse.
- **Fix:**
  1. If a major heading follows a section break, **do not** set `pageBreakBefore` — the section break already starts the new page.
  2. Use `pageBreakBefore` only when there is **no** preceding section break and you still need a new page.
  3. Remove consecutive empty body paragraphs that sit between a section break and the next heading.
  4. Treat section/page breaks as counting for ~1 spacing unit so you do not also stack large `before` spacing on top of the break.
- **Doesn't apply when:** The heading does not follow a section break (then `pageBreakBefore` is the right tool for "always start major headings on a new page"). Also does not apply to intentional blank pages (none in this thesis).

### Trailing blank page at end of document
- **Problem:** PDF ended with an empty (or near-empty) final page after the last real content (e.g. after Appendix C).
- **Root cause:** Not the same as the mid-doc “heading after section break” bug. An **extra** section break and/or empty paragraphs sat **after the last content**, so Word/LibreOffice emitted one more page. A single body-level `w:sectPr` at the end of `w:body` is normal and required; a *second* section boundary or leftover empties after content is what creates the trailing blank.
- **Fix:**
  1. Remove empty paragraphs after the last content paragraph.
  2. Remove any redundant trailing section break so only the standard final body `sectPr` remains.
  3. Re-export PDF and confirm the last page still has text.
- **Doesn't apply when:** You intentionally want a blank back page. Also different from mid-document blanks caused by `pageBreakBefore` + section break before a major heading (see sibling entry under this umbrella).


### Half-empty page — next section will not fill remaining space
- **Problem:** A page ends after a table or short paragraph with a large empty lower half; the next section heading (e.g. MARKING FALSE POSITIVES, UNHEDGED ASSERTIONS) starts alone at the top of the **next** page. User sees “wasted space” and thinks a page-break flag is set.
- **Root cause (geometry, not a hidden break):** The next **block** (heading + intro + full table, or heading + long keepNext chain) is **taller than the free space** left on the current page. Word/LibreOffice will not leave a section title at the bottom with almost no table under it, so the **whole block** moves to the next page. Char-count of extracted PDF text understates table height; a “half-empty” page may have only ~30–40% of a page free while the next block needs ~70–100%.
- **Fix:**
  1. **Diagnose first:** Measure free space vs height of the *entire* next block (heading + following paras + table). If block > free space, a shared page is impossible without shortening content.
  2. Prefer **v81 row-wise table splits**: `cantSplit` on each row so rows stay intact, but the **table may continue** on the next page with later rows; the **following section can start mid-page** after the previous table’s last rows if room remains.
  3. Avoid `keepNext` chains that glue heading + *all* bullets + *entire* table into one unbreakable unit when the table is multi-row and tall.
  4. Shorten overlong intro lines under the heading (e.g. Strike-through FP instruction) if they block the table from starting mid-page.
  5. Reference layout that worked: **Draft_081** / restored block in **Draft_091** (DECISION + MARKING + FP rows shared one page).
- **Doesn't apply when:** The next block truly fits in the residual space but still won’t move — then check `pageBreakBefore`, empty paragraphs, or section breaks (true blank-page bugs above).

### keepNext chain forces blank lower half / section on new page
- **Problem:** Clearing nothing still leaves MARKING FALSE POSITIVES, UNHEDGED ASSERTIONS, or FULL CODEBOOK starting a new page while the previous page looks underfilled.
- **Root cause:** Long `w:keepNext` chains (heading → bullets → table → next heading) make Word/LO try to keep the **whole chain** together. If it doesn’t fit, the chain jumps, leaving empty space. Stacked with `before=120` on section heads and `tblHeader` on every row, Appendix A repeatedly “opened new pages.”
- **Fix:**
  1. Do **not** keepNext across an entire appendix subsection. Use keepNext only for **heading + first line** (or heading + table start), not heading + six bullets + full table.
  2. For MARKING / UNHEDGED specifically: allow the section to **start mid-page**; let the FP/Unhedged **table** split by **complete rows** (`cantSplit` per row).
  3. Cap section-head `before` spacing (e.g. 40–60, not 120) in dense appendix codebooks.
- **Doesn't apply when:** A single short heading must stay with a small 2-row table that fits; keepNext is fine there.

### Orphan nearly-blank page after a codebook section
- **Problem:** PDF page with only one short line (e.g. “Optional Rejected Candidates tab…”) or a lone UNHEDGED heading — looks like a blank page.
- **Root cause:** Empty body paragraph between table and next heading, and/or keepNext + tall table pushing a short trailing paragraph alone onto the next page.
- **Fix:** Remove empty paragraphs between table and following text. Clear keepNext on trailing one-liners. Ensure the trailing line can stay on the previous page with the table’s last rows.
- **Doesn't apply when:** Appendix B legitimately starts a new major section (section break) — that is intentional.

## OOXML pack / validation

### `pPr` child order / invalid elements fail pack
- **Problem:** `pack.py` validation failed (e.g. `wordWrap` “element is not expected”); docx did not update; PDF still showed old formatting.
- **Root cause:** `w:pPr` children must follow the schema order; inserting elements in the wrong order or unsupported positions fails validation.
- **Fix:** After editing `pPr`, **reorder children** to the known sequence (keepNext → pageBreakBefore → spacing → jc → … → sectPr). Prefer not adding optional elements (like `wordWrap`) unless required and ordered correctly. Always confirm pack validation PASSED before trusting the PDF.
- **Doesn't apply when:** Editing only run-level `rPr` (fonts/sizes) with no `pPr` changes.

## Spacing (headings)

### Major heading “3-after” spacing not visible
- **Problem:** XML showed `before=360/720` and `after=360/720` on major headings, but the PDF still looked like only ~1 blank line after INTRODUCTION, METHODOLOGY, etc.
- **Root cause:** `w:keepNext` was set on major chapter headings. Word/LibreOffice keep the heading with the following paragraph and **collapse or hide the after-spacing**, so the gap never shows.
- **Fix:** Turn **`keepNext` OFF** on chapter majors (INTRODUCTION, METHODOLOGY, RESULTS…, CONCLUSIONS AND RECOMMENDATIONS, REFERENCES). Keep `keepNext` for minors/captions where orphan control matters. Use a consistent unit scale (here: 1 space = 240 twips, 3 spaces = 720).
- **Doesn't apply when:** You intentionally want a heading glued to the next line (e.g. caption above a table); then `keepNext` is correct and you accept little/no after-gap.

### Minor “1-before” looked the same as major “3”
- **Problem:** Minors and majors appeared to have the same gap length even when XML differed.
- **Root cause:** Inconsistent units (minor before=120 while major=720), plus the old rule “after a major, zero the minor’s before so only major after counts,” which erased the minor’s own 1-space.
- **Fix:** Use one scale: **1 = 240 twips, 3 = 720**. Minors: `before=240`, `after=0`. Majors: `before=720`, `after=720` (with `keepNext` off). Do not zero minor before just because a major precedes it unless the user explicitly wants only the major’s after-gap.
- **Doesn't apply when:** User specifies a different visual scale (e.g. appendix majors at 1-space so Quick-Reference fits one page).

## Tables

### Table caption splits from table body (LibreOffice PDF)
- **Problem:** “Table N” sat alone at the bottom of a page; table body started on the next page. `keepNext` on the caption did not help in LibreOffice export.
- **Root cause:** LibreOffice often **ignores `keepNext` across a paragraph → table** boundary. `pageBreakBefore` on the caption alone can still leave an orphan caption if the table doesn’t fit.
- **Fix:** Prefer **external** captions (paragraph above the table), not labels embedded in the first header cell (embedding broke column layout). Accept that LO may still split caption/table sometimes; avoid putting the label *inside* the table. Use smaller table font/single cell line-spacing so tables fit more often on the same page as the caption.
- **Doesn't apply when:** Exporting only with Microsoft Word (keepNext p→tbl is more reliable there).

### Do not embed table labels inside header cells
- **Problem:** Putting “Table 1: Title | Category” into the first header cell fixed caption orphans but **messed up the whole table** (wrong first-column text, layout).
- **Fix:** Keep **Table N + title as normal paragraphs above the table**. Restore pure column headers in the first row.
- **Doesn't apply when:** A template deliberately uses a single-row title band as part of the table design (not this thesis).


### tblHeader on every row breaks pagination
- **Problem:** Codebook tables forced odd page breaks, header-looking repeats, or whole tables jumping; UNHEDGED / Decision tables misbehaved across drafts 074–088.
- **Root cause:** `w:tblHeader` was set on **every** row (not only the first). Processors treat multiple header rows as repeating header bands and change break behavior.
- **Fix:** **`tblHeader` only on row 0.** Body rows: no tblHeader. Re-check after any table rewrite or “copy formatting” pass.
- **Doesn't apply when:** A table is intentionally designed with a multi-row header band that must repeat (rare; not used in this thesis codebook).

### cantSplit = no mid-row break; table may still split between rows (v81 pattern)
- **Problem:** Confusion between “rows must not split” and “the whole table must stay on one page.” Agents either set cantSplit and then wondered why sections still wouldn’t fill residual space, or removed cantSplit and got mid-cell splits.
- **Root cause:** `w:cantSplit` on a **row** means that **row** is atomic. The **table can still break between rows**. That is the correct behavior for filling the bottom of a page with as many full rows as fit.
- **Fix (reference: Draft_081, reapplied Draft_091):**
  1. Set **`cantSplit` on every data row**.
  2. Set **`tblHeader` only on the first row**.
  3. Do **not** require the entire multi-row table to fit before the next section can start.
  4. Target flow: previous table’s last rows + next section heading + first rows of next table on the **same page** when space allows (e.g. Decision Rules + MARKING FALSE POSITIVES + FP rows on one page).
- **Doesn't apply when:** A 2–3 row table must stay with its caption and truly fits — then keeping the small table unsplit is fine.

### Appendix A “mess” after incremental spacing edits
- **Problem:** Repeated drafts (073–090) oscillated on QR/QRL fonts, keepNext, blank pages, and MARKING/Unhedged page breaks; each “fix” regressed another part of Appendix A.
- **Root cause:** Patching one symptom (gap after HEDGE TYPE, QR font, blank page) without a single **reference draft** for table-split + density. Content length also drifted (e.g. longer Strike-through intro in later drafts made the FP block taller than residual space).
- **Fix:**
  1. **Read `lessons.md` (this file) before editing Appendix A pagination.**
  2. Use **Draft_081** (or Draft_091’s restored HEDGE TYPE→Unhedged block) as the **layout reference** for Decision / MARKING / UNHEDGED table splits.
  3. Use **Draft_084** as the **QR/QRL font & spacing** reference (sz 22 body / 24 heads; tight after on bullets).
  4. After any Appendix A edit: export PDF and check (a) no page with ≪500 extractable chars mid-appendix, (b) MARKING not alone after a half-empty Decision page, (c) tables break only between rows.
- **Doesn't apply when:** User explicitly asks for a different appendix structure (e.g. each FP code on its own page).


### Format reference ≠ section arrangement
- **Problem:** Using an older draft (e.g. v81) as a formatting reference, the agent also **reordered** Appendix A sections (e.g. moved CODING SHEET before Full Codebook) because that older draft had a different intentional structure.
- **Fix:** When the user says follow an older draft for **formatting** (spacing, fonts, borders, cantSplit, tblHeader), copy **those rules only**. Do **not** change section order unless the user explicitly asks to rearrange. Latest draft order is intentional when it differs from older drafts.
- **Doesn't apply when:** User explicitly says to restore an older draft’s structure or merge layouts section-for-section.


### Major chapter page breaks stripped during appendix edits
- **Problem:** CONCLUSIONS AND RECOMMENDATIONS and REFERENCES no longer started on a new page after appendix-focused OOXML edits. Body chapters that use section breaks (INTRODUCTION, METHODOLOGY, RESULTS) were fine; chapters that used an empty paragraph with `w:br type=page` lost that break when empty paras were bulk-removed.
- **Fix:** Restore empty page-break paragraphs before CONCLUSIONS AND RECOMMENDATIONS and REFERENCES (v81 pattern). Do **not** bulk-delete empty paragraphs that contain `w:br type="page"`. Before deleting empties, skip any with a page break. Full pass vs a known-good draft (e.g. v81) for major heading page starts after any body-wide cleanup.
- **Doesn't apply when:** Institution requires continuous chapter flow with no page break before conclusion/references.


### Only what is explicitly asked — no drive-by extras
- **Problem:** Agent “helps” beyond the instruction (extra notes under Combined Example with marks, rearranging sections when only formatting was requested, bulk cleanups that strip page breaks). Each extra creates new errors and repeat debugging.
- **Fix:** Execute the stated request only. No added notes, no unrequested rearrangement, no opportunistic formatting elsewhere. Match reference drafts for the property named (e.g. marks on example sentence only), not for optional extras.
- **Doesn't apply when:** User explicitly says to do a full pass, audit, or “fix everything related.”


### Do not strip formats outside the named section
- **Problem:** A stylistic request (e.g. fix bold in QR, restore Combined Example marks) is treated as a document-wide format pass. Highlights, strikes, page breaks, or spacing elsewhere get removed or normalized, then hours go to re-debugging.
- **Fix:** Scope = only the section(s) named in the user message. Never remove formats universally unless asked. If scope is unclear, ask before editing.
- **Doesn't apply when:** User explicitly requests a full-document or universal format change.

## Title page

### Double spacing pushes name/date to page 2
- **Problem:** With body double spacing (line=480) and the full empty-line structure, name and date overflowed to page 2.
- **Fix:** Title page only: use **1.5 line spacing** (`line=360`). Tune empties before the name (about **5** at 1.5) so name + date stay on page 1 at the bottom. Body stays double. Section break after the date; INTRODUCTION at top of page 2 with `before=0`.
- **Doesn't apply when:** Institution requires double spacing on the title page and allows a two-page title block.
