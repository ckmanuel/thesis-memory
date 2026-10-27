# Thesis formatting (binding)

This file is the **binding** layout spec for the working thesis body.

**Working file:** `thesis/003_ThesisProposal_Draft_127_body.docx` (overwrite in place).

If chat instructions and this file conflict, **this file wins** for layout.

Last updated: 2026-10-27 (blank-slate pass)

---

## Versioning

- **Do not inflate draft numbers** for format-only or routine edits.
- Overwrite `Draft_127_body.docx` only.
- New draft ID only when the user explicitly asks.
- **No PDF** unless the user asks.

---

## Global

| Property | Value |
|----------|--------|
| Font (every run) | **Georgia** |
| Body / headers / references line spacing | **Double** (`w:line` = 480) |
| Title page line spacing | **1.5** (`w:line` = 360) — **do not change** title-page blank structure |
| Prefer | **Section break (nextPage)** over page break |
| Prefer | **Empty spacer paragraph** over paragraph space-before/after |
| Content spacing | before = 0, after = 0 on text; gaps via empty spacers only |

---

## Title page

- Centered
- Title lines: **14 pt bold**
- Other lines: **12 pt regular**
- Line spacing: **1.5**
- Keep existing blank structure

---

## Breaks

- Chapter starts: `w:sectPr` `nextPage` + `titlePg` (hidden page numbers on first page of section)
- Place sectPr on the **empty spacer immediately before** the major header — **not** on body text
- No run-level page breaks

---

## Major headers

Examples: INTRODUCTION, METHODOLOGY, RESULTS…, CONCLUSIONS…, REFERENCES, APPENDIX A/B/C

| Property | Value |
|----------|--------|
| Font | Georgia **14 bold** |
| Alignment | **Center** |
| Text spacing | before/after **0** |
| Empty spacers **before** | **3 plain on the new page** above the major. Section break is a **separate** empty spacer *before* those three (ends previous section). Order: `[break spacer]` → `[plain]` ×3 → major |
| Empty spacers **after** | **3** |
| Pagination | Hidden on section first page (`titlePg`) |

---

## Minor headers

### Subsections (bold)

Background of the Study, Statement of the Problem, Research Framework, Significance of the Study, Scope and Limitations, Definition of Terms, Research Design, Research Context, Research Process, Research Corpus, Inclusion Criteria, Exclusion Criteria, Conclusions, Recommendations, Ethical Considerations, etc.

| Property | Value |
|----------|--------|
| Font | Georgia **12 bold** |
| Alignment | Left |
| Indent | None |
| Spacers before | **1** (skip if already follows major’s after-spacers) |
| Spacers after | **0** |
| keepNext | **Yes** |

### Thematic (italic)

Part I–IV titles, discussion theme heads

| Property | Value |
|----------|--------|
| Font | Georgia **12 italic** (not bold) |
| Alignment | Left |
| Indent | None |
| Spacers before | **1** (same rule as bold minors) |
| Spacers after | **0** |
| keepNext | **Yes** |

---

## Body

| Property | Value |
|----------|--------|
| Font | Georgia **11** |
| Alignment | **Justify** |
| First-line indent | **0.5 in** (720 twips) |
| Empty spacers between body paragraphs | **0** |
| Empty spacers before/after each table | **1** each |
| Line spacing | Double |

Bullets: left 0.5 in, hanging 0.25 in — not body first-line.

---

## Tables

| Property | Value |
|----------|--------|
| Cell font | Georgia **11**, center horizontal + vertical |
| Cell line spacing | **1.15** (`w:line` = 276) |
| Cell fills | **Keep** (do not strip header/totals colors) |
| cantSplit | Every row |
| Borders | Open-sided (no vertical) |
| Header row | Thick top sz 18 + thin bottom sz 4 |
| Last row | Thick bottom sz 18 |
| Totals row | Thin top sz 4 + thick bottom |
| Middle rows | No cell borders |
| Label (`Table N`) | Georgia 11 bold left; line **1.5**; keepNext |
| Caption title | Georgia 11 regular left; line **1.5**; keepNext |

---

## Definition of Terms

- Alphabetical by term name
- Term name **bold** through first comma; rest regular
- Body paragraph rules otherwise

---

## References

- Hanging indent **0.5 in**
- APA, alphabetical
- Do not split a reference mid-entry across intentional isolation (keepLines ok on entry)

---

## Appendix

- **Highlights, strikes, shading, function colors: do not alter**
- Spacing/fonts only, same rules as body/majors

---

## Intentional bold (keep)

- Major/minor headers as specified
- Table numbers on caption lines
- Significance leads: `For writing instructors…`, `For academic writing researchers…`, `For the BAELS program…`, `For future researchers…`
- Research Process step labels
- Definition of Terms: term name only
- Table header row text

**Bold spill:** entire long body paragraph bold → clear (except term name pattern).
