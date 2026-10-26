# Thesis formatting (binding)

This file is the **binding** format spec for `thesis/003_ThesisProposal_Draft_*_body.docx`.
Any format pass must follow it. If prose and this file conflict, **this file wins** for layout.
Do not invent parallel rules in chat without updating this file.

Last updated: 2026-10-26 (Draft_128 pass)

---

## Global

| Property | Value |
|----------|--------|
| Font (all runs) | **Georgia** |
| Line spacing (body, headers, tables, references) | **Double** (Word line = 480, auto) |
| Line spacing (title page only) | **1.5** (Word line = 360, auto) |
| Em dashes / semicolons in thesis prose | **Forbidden** (existing house rule) |

---

## Title page

- Alignment: **center**
- Main title lines: **14 pt, bold**
- All other title-page lines: **12 pt, regular**
- Line spacing: **1.5**
- No first-line indent
- Keep existing vertical rhythm (do not reflow title-page blank structure)

---

## Major headers

Examples: `INTRODUCTION`, `METHODOLOGY`, `RESULTS, ANALYSIS, AND DISCUSSION`, `CONCLUSIONS AND RECOMMENDATIONS`, `REFERENCES`, `APPENDIX A…`

| Property | Value |
|----------|--------|
| Font | Georgia **14 bold** |
| Alignment | **Center** |
| Space before | **3** line units (720 twips) |
| Space after | **3** line units (720 twips) |
| Indent | None |
| Pagination | **Page break before** each major header (chapter opener). Page-number suppression on opener pages requires section breaks in Word if the school template demands hidden pagination. |

---

## Minor headers

### Subsections (bold)

Examples: Background of the Study, Statement of the Problem, Research Framework, Significance of the Study, Scope and Limitations, Definition of Terms, Research Design, Research Context, Research Process, Research Corpus.

| Property | Value |
|----------|--------|
| Font | Georgia **12 bold** |
| Alignment | **Left** |
| Space before | **1** line unit (240 twips), **or 0** if the previous paragraph was a major header |
| Space after | **0** |
| Indent | **None** (no first-line, no left indent) |
| Keep with next | **Yes** (do not leave header alone at page bottom) |

### Themed sections (italic)

Examples: `Part I:…`–`Part IV:…`, literature-review theme heads, discussion theme heads
(e.g. Function Profile…, How Programs Word Caution). **Not bold.**

| Property | Value |
|----------|--------|
| Font | Georgia **12 italic** (**not bold**) |
| Alignment | **Left** |
| Space before / after / indent / keep-next | Same as subsections |

**Do not** bold thematic titles when clearing indent or during format passes.

---

## Body

| Property | Value |
|----------|--------|
| Font | Georgia **11** |
| Alignment | **Justify** |
| First-line indent | **0.5 inch** (720 twips) |
| Space between body paragraphs | **0** |
| Space before body paragraph that follows a table | **1** line unit (240 twips) |
| Line spacing | Double |

### Intentional bold in body (keep; nothing else)

- Significance stakeholder leads (`For writing instructors…`, etc.)
- Research Process step labels (`a. Requesting Permission.` …)
- Definition of Terms: **term name** only (text before the first comma)
- Inclusion / Exclusion / Ethical Criteria labels
- Table numbers (`Table 1`, `Table 2`, …)
- Table header row (and totals row label cells as specified under Tables)

**Bold spill rule:** If an entire long body paragraph is bold, clear it. Never leave full-paragraph bold on ordinary body text.

---

## Tables

| Property | Value |
|----------|--------|
| Cell font | Georgia **11**, **center** |
| Row break | **cantSplit** on every row (no mid-row page split) |
| Label + caption | **Keep with next** through to the table (do not isolate `Table N` or the caption title) |
| Caption font | Georgia **11**, **left**; `Table N` line **bold**; title line regular |
| Vertical borders | **None** (open-sided) |
| Header row | Thick top **sz 18** + thin bottom **sz 4** |
| Middle rows | No cell borders |
| Last row | Thick bottom **sz 18** |
| Totals row | **Top** border (thin sz 4) in addition to last-row rule when the totals row is last |
| Full grid | Removed |

---

## Definition of Terms

- Entries in **alphabetical order** by term name
- Term name **bold**; rest of entry regular
- Body paragraph rules otherwise apply

---

## References

| Property | Value |
|----------|--------|
| Order | **Alphabetical** by first author surname (APA) |
| Indent | **Hanging 0.5 inch** |
| Font | Georgia **11** |
| Alignment | Justify |
| Line spacing | Double |
| APA | Uniform APA 7 (italics on journal/book titles preserved in runs) |

---

## Pass checklist (every format run)

1. Apply Georgia to every run.
2. Title page vs body line spacing split.
3. Classify each paragraph: title / major / minor bold / minor italic / table label / table caption / body / reference / empty.
4. Bold-spill scan on body.
5. Table borders + cantSplit + caption keep-next.
6. Definition of Terms alphabetical.
7. References alphabetical + hanging indent.
8. Overwrite working body `Draft_124_body.docx` only (see Versioning). No PDF unless asked.

---

## Versioning (binding)

- **Do not inflate draft numbers** for format-only or routine edits.
- **Working body file:** `thesis/003_ThesisProposal_Draft_124_body.docx` — **overwrite in place**.
- New draft IDs only when the user explicitly asks for a new draft, or for a major content revision they approve.
- **No PDF** in the default pass. Produce `.docx` only unless the user asks for a PDF.

