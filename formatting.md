# Thesis formatting (binding)

This file is the **binding** layout spec for the working thesis body.

**Working file:** `thesis/003_ThesisProposal_Draft_127_body.docx` (overwrite in place).

If chat instructions and this file conflict, **this file wins** for layout. Do not invent parallel format rules in chat without updating this file first.

Last updated: 2026-10-27

---

## Versioning

- **Do not inflate draft numbers** for format-only or routine edits.
- Overwrite `Draft_127_body.docx` only.
- New draft ID only when the user explicitly asks, or for a major content revision they approve.
- **No PDF** unless the user asks for one. Docx only by default.

---

## Global

| Property | Value |
|----------|--------|
| Font (every run) | **Georgia** |
| Body / headers / tables / references line spacing | **Double** (Word `w:line` = 480, `auto`) |
| Title page line spacing | **1.5** (Word `w:line` = 360, `auto`) |
| Em dashes and semicolons in thesis prose | **Forbidden** (house rule; rephrase) |

---

## Title page

- Alignment: **center**
- Main title lines: **14 pt, bold**
- All other title-page lines: **12 pt, regular**
- Line spacing: **1.5**
- No first-line indent
- Do not reflow title-page blank structure
- End of title page: **next-page section break** on the last title-page paragraph (e.g. date line). That is what starts INTRODUCTION. Do not also put `pageBreakBefore` on INTRODUCTION.

---

## Breaks and pagination (critical)

**Use only one break type for chapter starts: next-page section break.**

| Rule | Detail |
|------|--------|
| Chapter start | Put `w:sectPr` with `w:type val="nextPage"` on the **paragraph immediately before** the major header |
| Major header itself | **No** `pageBreakBefore`. **No** `sectPr` on the major paragraph |
| Why | `pageBreakBefore` alone suppresses **space before** at the top of the page in Word. INTRODUCTION looked correct because the title page already used a section break. Other majors must match that pattern |
| Never | Section break **and** page break on the same chapter boundary |
| Never | Mid-body section breaks or run-level page breaks inside ordinary body paragraphs (these isolated Token after Softening) |
| Body flow | Softening, Token, and other sequential glossary/body lines: **no** keepNext chains, **no** keepLines packs, **no** embedded sectPr. Natural flow only |

---


## Vertical spacing (binding)

**Prefer empty spacer paragraphs over space-before / space-after on text.**

| Rule | Detail |
|------|--------|
| Default | Content paragraphs use **before = 0** and **after = 0** (line spacing still applies: body double `480`, tables single `240`) |
| Gaps | Insert an **empty spacer paragraph** (no text, line `480` auto, before/after `0`, no indent) where a blank line is needed |
| Where spacers are used | After tables; before major headers when a gap is required; before minor labels when a gap is required; after majors when a gap is required; other visible gaps that must survive Word’s table/header quirks |
| Collapse | Consecutive empty spacers → **one** |
| Avoid | Relying on space-before / space-after on body, caption, or appendix text to create vertical gaps (Word often ignores space-before after tables and can stack unevenly) |

Appendix spacing follows the same rule (see also below if present).

## Major headers

Examples: `INTRODUCTION`, `METHODOLOGY`, `RESULTS, ANALYSIS, AND DISCUSSION`, `CONCLUSIONS AND RECOMMENDATIONS`, `REFERENCES`, `APPENDIX A…`

| Property | Value |
|----------|--------|
| Font | Georgia **14 bold** |
| Alignment | **Center** |
| Space before / after | **0** on the header text itself |
| Vertical gap | **Empty spacer paragraph(s)** before and/or after the major (see Vertical spacing) |
| Indent | **None** |
| Break | Section break on **previous** paragraph only (see Breaks) |

Apply these values to **every** major, not only INTRODUCTION.

---

## Minor headers

Two kinds. Both are left-aligned, no indent, space before/after 0; gap via empty spacer before the minor when needed (not if it immediately follows a major with no gap wanted), **keep with next** so the header cannot sit alone at the bottom of a page without the following paragraph.

### Subsections (bold)

Examples: Background of the Study, Statement of the Problem, Research Framework, Significance of the Study, Scope and Limitations, Definition of Terms, Research Design, Research Context, Research Process, Research Corpus, Inclusion Criteria, Exclusion Criteria, Conclusions, Recommendations.

| Property | Value |
|----------|--------|
| Font | Georgia **12 bold** (not italic) |
| Alignment | Left |
| Indent | **None** |
| Keep with next | **Yes** (header only) |

### Themed sections (italic)

Examples: `Part I:…`–`Part IV:…`, literature-review theme heads, discussion theme heads (Function Profile…, How Programs Word Caution, Open Readings, etc.).

| Property | Value |
|----------|--------|
| Font | Georgia **12 italic** (**not bold**) |
| Alignment | Left |
| Indent | **None** |
| Keep with next | **Yes** (header only) |

**Do not** bold thematic titles when clearing indent or during format passes.

**Do not** put empty paragraphs between a minor header and its first body paragraph (empty next breaks keep-with-next).

---

## Body

| Property | Value |
|----------|--------|
| Font | Georgia **11** |
| Alignment | **Justify** |
| First-line indent | **0.5 inch** (720 twips) |
| Space between body paragraphs | **0** |
| Space after every table | Word often **ignores** space-before on the paragraph after a table. Insert an **empty spacer paragraph** (double line, no text) immediately after every table so a blank line always shows |
| Line spacing | Double |

### List-like lines (not body first-line)

Bullets (`• …`) and numbered RQ lines (`1. …`): left indent 0.5 in, hanging 0.25 in. **Not** first-line indent of 0.5 in as if normal body.

### Intentional bold in body (only these)

- Significance stakeholder leads, and **only** these starts: `For writing instructors…`, `For academic writing researchers…`, `For the BAELS program…`, `For future researchers…`
- Research Process step labels (`a. Requesting Permission.` …)
- Definition of Terms: **term name** only (through first comma)
- Inline `Inclusion Criteria.` / `Exclusion Criteria.` / `Ethical Considerations.` labels when used as lead-in
- Table numbers on caption lines (`Table 1`, …)
- Table header row (and totals row labels)

**Never** treat a generic `For …,` sentence (e.g. Scope “For a manually coded…”) as a Significance lead.

**Bold spill rule:** If an entire long body paragraph is bold, clear it.

---

## Figure 1

Order under Research Framework:

1. Grounding paragraph  
2. Overview paragraph (source jobs)  
3. **Figure 1** label (11 bold, left)  
4. Caption title (11 regular, left)  
5. Image (centered)  
6. Remaining framework body (coding path)

Caption label + title: keep with next through the image. Do not leave the drawing after later body paragraphs.

---

## Tables

| Property | Value |
|----------|--------|
| Cell font | Georgia **11**, **horizontal center** |
| Cell vertical align | **Center** (`w:vAlign` = center) |
| Cell line spacing | **Single** (240), not double. Double line boxes pin text to the top of the line and look “forced up” even with vAlign center |
| Cell margins | Equal top/bottom/left/right (`tcMar`) |
| Cell paragraph spacing | Small equal before/after (e.g. 60); no first-line indent |
| Row break | **cantSplit** on every row |
| Label + caption | **Both** lines get `keepNext` so neither isolates above the table |
| Caption line spacing | **1.5** (`w:line` = **360** auto) on Table/Figure **label and title only** — not on cell text |
| Caption (binding, **all** tables) | Same rules for **whole-number** (`Table 1`) and **decimal** (`Table 4.1`, `5.1`, …) IDs. No special case for sub-tables. |
| Caption — `Table N` line | Georgia **11**, **bold**, **left**, no indent (`firstLine`/`left` = 0). Spacing: before **240**, after **0**, line **480** auto. `keepNext` |
| Caption — title line | Georgia **11**, **regular** (not bold), **left**, no indent. Spacing: before **0**, after **240**, line **480** auto. `keepNext` |
| Caption — forbidden | Body first-line indent; justified (`both`); treating decimal labels as ordinary body paragraphs |
| Vertical borders | **None** (open-sided) |
| Header row | Thick top sz **18** + thin bottom sz **4** |
| Header fill | **D9E2F3** (light blue; same as Timeline table) |
| Totals row fill | **F2F2F2** (light gray) when the row is a Total/Totals row |
| Body rows fill | None (no shading) |
| Middle rows | No cell borders |
| Last row | Thick bottom sz **18** |
| Totals row | Thin top sz **4** as well when it is the last row |

---

## Definition of Terms

- Alphabetical by term name  
- Term name **bold**; rest regular  
- Otherwise normal body paragraphs (first-line indent, double spacing)  
- **No** keepNext / keepLines packs on glossary entries  
- **No** section break inside a glossary paragraph  

---

## References

| Property | Value |
|----------|--------|
| Order | Alphabetical by first author surname (APA) |
| Indent | Hanging **0.5 inch** |
| Font | Georgia **11** |
| Alignment | Justify |
| Line spacing | Double |
| APA | Uniform APA 7 (italics on journal/book titles kept in runs) |

---

## Format-pass checklist (required every time)

1. Georgia on every run.  
2. Title page 1.5 vs body double.  
3. Classify: title / major / subsection bold / thematic italic / table label / caption / body / bullet-RQ / reference.  
4. **Breaks:** next-page section break only on the paragraph before each major; strip `pageBreakBefore` from majors; strip mid-body sectPr and run-level page breaks.  
5. Major: 14 bold center, before/after 720.  
6. Minor: no indent; subsection bold 12; thematic italic 12 not bold; keepNext on header only.  
7. Body bold-spill scan; intentional leads only.  
8. Tables: open borders, cantSplit, caption keep-next.  
9. Definition of Terms alphabetical; natural flow.  
10. References alphabetical + hanging.  
11. Overwrite `Draft_127_body.docx` only. No PDF unless asked.  
12. After the pass, **verify** majores: no `pageBreakBefore`, prev has nextPage sectPr, before=720.

---

## Known failure modes (do not repeat)

| Mistake | Result |
|---------|--------|
| `pageBreakBefore` on majors instead of section break before them | Space before shows on INTRODUCTION only |
| Section break + page break together | Conflicts / uneven spacing |
| `sectPr` inside Softening or other body lines | Next line (e.g. Token) starts a new section alone |
| keepNext on long body chains | Empty space and “new section” look |
| Bolding all minor heads when fixing indent | Thematic titles wrongly bold |
| Generic `For …` bold matcher | Scope prose false bold |
| Inflating Draft_125+ for format | Forbidden; overwrite 124 |

## Appendix spacing

Same as **Vertical spacing (binding)**: spacers only; no space-before/after on appendix text for gaps.

