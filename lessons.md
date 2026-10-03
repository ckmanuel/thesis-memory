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

