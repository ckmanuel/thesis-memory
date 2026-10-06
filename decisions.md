# Key Decisions

Append-only log. Newest at top. Don't edit past entries — supersede with a new entry.

**Three sources of truth, no overlap:**
1. `chat_history/` — verbatim transcript.
2. `decisions.md` — durable decisions (this file).
3. `context.md` Recently Completed — short-term pointer list.

No parallel summary files. They drift.

**Memory file routing:**
- Facts → `knowledge.md`
- Preferences → `preferences.md`
- Decisions → `decisions.md`
- Current focus → `context.md`
- Projects → `projects.md`
- Verbatim record → `chat_history/`

<!--
Entry template:

## YYYY-MM-DD — <Short title>
- **Context:** <what triggered this>
- **Decision:** <what was decided>
- **Rationale:** <why>
- **Status:** active | superseded by <date>
-->

## 2026-10-04 — Excel: style Outcome Type + P/DO tabs to match other sheets
- **Context:** User: last 2 added tabs are bare bones; match design of other tabs.
- **Decision:** Overwrite `007_CompiledResult_Draft_005.xlsx`.
  - Outcome Type + P and DO Functions restyled like Hedges/Unhedged/Rejected: col A spacer, title B2 (14pt bold navy), subtitle B3, dark header row (1B2A4A / white), alternating F7F7F5 rows, thin borders, freeze B6, Calibri 11.
  - Outcome Type: deduped to 60 abstracts (removed junk “Binary” / note rows).
  - P/DO: note rows highlighted (FFF2CC).
- **Status:** active.

## 2026-10-04 — Draft_039: tighten Scope/Results repetition
- **Context:** Reviewer comment: sampling, limitations, and coding restated across Scope, Methodology/Corpus, Results, Appendix A.
- **Decision:** Overwrite Draft_039.
  - Scope: cut full stratified-sampling write-up; point to Research Corpus for design, intervals, inclusion/exclusion; shortened sample-size justification (comps pointed to Research Corpus).
  - Part III: shortened function paragraph (result first; less process restatement).
  - Appendix A left intact; Research Corpus remains sole full sampling home; Part IV still uses short Scope pointer only.
- **Status:** active. Working draft = Draft_039.

## 2026-10-04 — Draft_039: restore Significance lead-in bold pattern
- **Context:** User: only the first Significance body paragraph was wrongly fully bold; other paragraphs intentionally bold the first clause.
- **Decision:** Overwrite Draft_039. All four Significance body paragraphs now use bold lead-in + normal rest (including the first: “For writing instructors and thesis advisers at PSAU,” bold, remainder regular).
- **Status:** active. Working draft = Draft_039.

## 2026-10-04 — Draft_039: unbold Significance body + Inclusion/Exclusion Criteria
- **Context:** User: fix bolded text in Significance of the Study and Inclusion Criteria.
- **Decision:** Overwrite Draft_039. Set w:b val=0 on Significance body paragraphs (heading stays bold). Unbolded Inclusion Criteria and Exclusion Criteria paragraphs (were fully bold).
- **Status:** active. Working draft = Draft_039.

## 2026-10-04 — Draft_039: pull back Null/NS claim (Acs2-driven)
- **Context:** User arithmetic: Agri Null/NS without Acs2 averages 1.0, same as non-Null Agri; elevation is Acs2; no hedge-rate-by-outcome test; Agri has zero Binary (discipline × design entangled).
- **Decision:** Overwrite Draft_039. Part IV no longer calls Null/NS more central than density ranking; states elevation is carried by Acs2 (8 of 21 Null/NS hedges in Agri); remaining 13 average 1.0. Acs2 retained as single-case rescue-hedging example linked to intro. Notes Agri has zero Binary; formal outcome-type comparison not reported. Conclusions and Future Research aligned.
- **Status:** active. Working draft = Draft_039.

## 2026-10-04 — Draft_039: remove blank page before FULL CODEBOOK
- **Context:** User asked to check for blank pages and fix.
- **Decision:** Overwrite Draft_039 (per versioning policy). Removed empty paragraph that held a page-break `<w:br w:type="page"/>` immediately before FULL CODEBOOK, which already had `pageBreakBefore` — double break produced a fully blank page (was p.46). Document 111→110 pages. Title page and final page remain sparse by design.
- **Status:** active. Working draft = Draft_039.

## 2026-10-04 — Repo cleanup + draft versioning policy
- **Context:** User: repo cluttered with past drafts; only keep 2 latest; from now on overwrite current draft for small changes; new Draft_0xx only for major revisions. Later: include stylistic/format changes as overwrite.
- **Decision:**
  1. Removed all 003_ThesisProposal_Draft_001–037 (docx/pdf) and Preedit; removed 007_CompiledResult_Draft_001–004 and Preedit. Kept Draft_038, Draft_039, and CompiledResult_Draft_005.
  2. **Versioning policy (going forward):** Small/iterative edits — including stylistic and format changes (fonts, spacing, borders, table styling, heading tweaks) — overwrite the current working draft (and its PDF) in place. A new numbered Draft_0xx is created only for major revisions (structural rewrites, chapter-level changes, or when the user explicitly requests a new version). Keep at most the current + one previous numbered draft in the repo. Documented in `thesis/README.md`.
- **Status:** active. Working draft = Draft_039.

## 2026-10-04 — Draft_039: alphabetize Definition of Terms + match bold structure
- **Context:** User: added defs were fully bolded and not alphabetized.
- **Decision:** Draft_039 from Draft_038. Removed misplaced entries; re-inserted Chi-Square (after Claim), Cohen’s Kappa (after Clause-Level), Kruskal-Wallis (after Hedging) with the same two-run bold structure as existing terms (term name bold + body bold, matching Abstract/Normalized Frequency house style).
- **Status:** active. Working draft = Draft_039.

## 2026-10-04 — Draft_038: add Chi-Square, Cohen’s Kappa, Kruskal-Wallis to Definition of Terms
- **Context:** User asked to define stats terms with computation formulas, matching the Normalized Frequency style.
- **Decision:** Draft_038 from Draft_037. Added three entries after Normalized Frequency:
  - Chi-Square Test of Independence: χ² = Σ [(Oᵢ − Eᵢ)² / Eᵢ]; reported χ² = 5.07, df = 2, p = .079.
  - Cohen’s Kappa: κ = (Pₒ − Pₑ) / (1 − Pₑ); Landis & Koch bands; reported κ = 0.89.
  - Kruskal-Wallis Test: H = [12 / (N(N+1))] × Σ (Rⱼ² / nⱼ) − 3(N+1); reported H ≈ 7.39, p = .025 (on rates).
- **Status:** active. Working draft = Draft_038.

## 2026-10-04 — Draft_037: KW on rates + subtler caveats
- **Context:** User asked to apply per-100w rates (better than raw counts) and state caveats more subtly.
- **Decision:** Draft_037 from Draft_036.
- **Edits:**
  - Re-ran Kruskal-Wallis on per-abstract hedge rates (per 100 words): H ≈ 7.39, p = .025 (was H ≈ 6.84, p = .033 on counts). Rates preferred because VM abstracts average longer (~253 vs ~215–225 words).
  - Softened Part II caveat block: removed explicit “raw counts vs rates would be preferable,” “no post-hoc,” “p-values are fragile,” “not confirmatory evidence of a field-level difference.” Kept adviser clustering, spread, small/zero-inflated sample, exploratory framing.
  - Updated Part IV and Conclusions p-value references to rates version; Conclusions caveat shortened.
- **Status:** active. Working draft = Draft_037.

## 2026-10-04 — Draft_036: remove empty paragraphs before Part III pointer
- **Context:** User reported empty space before “As noted in Part III, an informal reading…”.
- **Decision:** Draft_036 from Draft_035. Removed three consecutive empty paragraphs left between the Outcome Type discussion and the Part III pointer (leftover from earlier limitation consolidation).
- **Also:** Generated and pushed Draft_035.pdf + Draft_036.pdf.
- **Status:** active. Working draft = Draft_036.

## 2026-10-04 — Draft_035: framing polish after Null/NS elevation
- **Context:** Ripple check after Draft_034 found light framing lags (not factual errors).
- **Decision:** Draft_035 from Draft_034.
- **Edits:**
  - Part IV opening: “three observable patterns” → “map frequency, function, and cross-disciplinary density”; contrasts framed as exploratory.
  - First Future Research paragraph: leads with Null/NS concentration + rescue-hedging + VM density instead of generic “disciplinary patterns.”
  - Methods Acs2: trimmed interpretive weight; points forward to Part IV for the full rescue/overclaiming reading.
- **Status:** active. Working draft = Draft_035.

## 2026-10-04 — Draft_034: elevate Null/NS+Acs2, consolidate limitations, fix stats/L3/curricula
- **Context:** User feedback: limitations over-repeated (Scope/Part II/IV/Conclusions); most interesting finding (Agri 14/21 Null/NS + Acs2 rescue-hedging) buried; KW on raw counts not rates; nested in advisers; no posthoc; L3 sites before Layer 3 defined; curricula claim uncited.
- **Decision:** Single-pass Draft_034 from Draft_033.
- **Edits:**
  - Elevated Null/NS concentration + Acs2 rescue as lead observation in Part IV and sharpened in Conclusions (links to intro overclaiming).
  - Consolidated Part IV limitation paragraph to one short Scope pointer.
  - Stats: noted KW on counts not rates, length variation, no posthoc/planned VM contrast.
  - Renamed Table 4 "L3 Sites" → "Unhedged sites"; updated prose reference.
  - Softened curricula claim: "rarely treated as a distinct rhetorical skill in many Philippine undergraduate writing courses" (no absolute "most universities").
- **Status:** active. Working draft = Draft_034.

## 2026-10-04 — Draft_033: Table 6 thick top/bottom borders (sz=18)
- **Context:** User: thick line isn’t there on Table 6. Remote Draft_032 lacked tblBorders.
- **Decision:** Draft_033 from remote Draft_032. Apply table-level borders matching Tables 2–5.
- **Edits:** tblBorders top+bottom single sz=18; sides/inside nil; tblStyle Table4; header cell bottom sz=4 only.
- **Status:** active. Working draft = Draft_033.

## 2026-10-03 — Draft_031: Table 6 exact format match (captions + cells)
- **Context:** User: copy other tables’ formatting to the dot — font size, line spacing, no exceptions.
- **Decision:** Draft_031 from Draft_030.
- **Edits (Table 6 only):**
  - Captions: Georgia 12pt; number bold; spacing before=720/after=0/line=480 (number), before=0/after=60/line=480 (title); centered — matches Tables 4–5.
  - Cells: Georgia 9pt (sz=18); paragraph spacing before=0 after=0 line=240; header bold + bottom border only; body no borders; Total row not bold (matches reference Tables).
- **Status:** active. Working draft = Draft_031.

## 2026-10-03 — Draft_030: Table 6 formatting matched to other Results tables
- **Context:** User: only Table 6 differed from the rest.
- **Decision:** Draft_030 from Draft_029. Restyle Table 6 to match Tables 2–5.
- **Edits:** Georgia 9pt (was Times New Roman 10pt); header bold + bottom border only; body cells no borders; no shading; Total row bold. Content unchanged.
- **Status:** active. Working draft = Draft_030.

## 2026-10-03 — Draft_029: Verb-tense pass against final-defense matrix
- **Context:** User supplied Verb Tense Matrix (proposal → final). Asked to check and correct mistakes.
- **Decision:** Draft_029 from Draft_028. Only one residual procedure-style future found.
- **Edits:** Ethics data-retention clause: “will be retained / will be permanently deleted” → “are retained / are permanently deleted” (standing practice, present tense).
- **Scan result:** Methodology already past-tense throughout (design, sampling, extraction, coding, ethics steps taken). Objectives/RQs present (allowed). Results use past for findings + present for table pointers (allowed). Conclusions mix past findings / present general claims (allowed). Recommendations use should / Future research should (allowed). No “proposed study” / proposal-stage future in main body. Appendix coded examples contain “will” only as source-text tokens.
- **Status:** active. Working draft = Draft_029.

## 2026-10-03 — Draft_028: Soften disciplinary-variation claims in Part I/II
- **Context:** User: the claim of disciplinary variation rests on Vet Med versus the other two; no clear Agriculture–Biology difference. Part I/II still said “varies meaningfully” and “substantial variation”; Conclusions already said limited evidence, mainly VM, Ag edge outlier-sensitive.
- **Decision:** Draft_028 from Draft_027.
- **Edits:**
  1. P131: “varies meaningfully” → differences most clearly in VM’s small total and low modal share.
  2. P134: Dropped “rhetorical style” speculation; type-mix contrast stated descriptively; Ag–Bio density difference flagged as marginal and outlier-sensitive; shared narrow repertoire emphasized.
  3. P140: “substantial variation” → differences driven mainly by VM’s lower rate.
- **Status:** active. Working draft = Draft_028.

## 2026-10-03 — Draft_027 + Excel Draft_005: Part I wording + FP-Gen fix
- **Context:** (1) “Scope notes” read as if Scope were a person. (2) “First-person or overtly stance-marking variants are rare by convention” was uncited and only partly covered the clause-level category (“it seems that” is not first-person). (3) Summary sheet listed FP-Gen = 38 (would total 63 FPs); Rejected Candidates and Coding Summary have FP-Gen = 33 / total 58.
- **Decision:** Draft_027 from Draft_026; CompiledResult Draft_005 from Draft_004.
- **Edits:**
  1. “Scope notes” → “The Scope and Limitations section notes.”
  2. Softened the rarity claim: science abstracts favor impersonal compact reporting; clause-level stance frames (first-person and impersonal) are uncommon in that register — no new citation required.
  3. Summary sheet FP-Gen 38 → 33 so it matches the 58 total elsewhere.
- **Note:** User also observed that “disciplinary variation” rests mainly on VM vs the other two, with no clear Ag–Bio difference (consistent with the Acs2 sensitivity check and the Conclusions’ “limited evidence… mainly Veterinary Medicine”). Not rewritten in this pass.
- **Status:** active. Working draft = Draft_027; spreadsheet = Draft_005.

## 2026-10-03 — Draft_026: Part I clause-level paragraph — genre + supervision, not sophistication
- **Context:** Part I read zero clause-level hedges as lack of syntactic sophistication (citing Hyland & Milton 1997). Codebook examples include “I think” / “in our view,” which science abstracts avoid by convention. Scope already attributes patterns to genre compression and adviser supervision.
- **Decision:** Draft_026 from Draft_025. Rewrite the Part I clause-level paragraph; light consistency pass on the Part III restricted-range sentence.
- **Edits:**
  1. Zero clause-level count now framed as consistent with abstract conventions and supervised products, not writer deficit.
  2. Explicitly notes that first-person / overt-stance variants are rare by genre convention.
  3. Hyland & Milton retained only for restricted range; institutional/genre setting is the more proximate explanation.
  4. Part III sentence aligned: restricted range cited, but genre + supervision remain proximate.
- **Status:** active. Working draft = Draft_026.

## 2026-10-03 — Draft_025: Outcome Type cross-tab added as Table 6
- **Context:** User noted the Outcome Type cross-tab lived only in the spreadsheet; the thesis gave it one paragraph and no table. If it carries the new argument, it belongs in Results.
- **Decision:** Draft_025 from Draft_024. Add Table 6 (Outcome Type by Discipline) in Part IV; revise the Outcome Type paragraph to point to the table.
- **Edits:**
  1. Inserted Table 6 (counts: Outcome Type × Discipline, with totals) after the Part IV intro paragraph.
  2. Rewrote the Outcome Type paragraph to refer to Table 6; kept the key contrasts (VM Binary 0.38 vs Bio Binary 1.57; Agri Null/NS 14/20) and the rejection of the binary-outcome account of VM density.
  3. Full per-abstract coding remains in the coding spreadsheet; table presents the aggregate cross-tab only.
- **Status:** active. Working draft = Draft_025.

## 2026-10-03 — Draft_024: Part II/IV consistency; outcome coding method; voice
- **Context:** Part II still explained VM density by binary outcomes while Part IV rejected that; future research still tied advisers to binary-outcome interpretation; outcome paragraph read like external feedback; no method for outcome coding.
- **Decision:** Draft_024 from Draft_023.
- **Edits:** Part II aligned with Part IV (binary account not supported). Future research → supervisory practice + Null/NS share. Outcome paragraph rewritten in plainer voice; Acs2 illustrates, does not prove. Methods: separate pass for outcome type from results language.
- **Status:** active. Working draft = Draft_024.

## 2026-10-03 — Draft_023 + Excel Draft_004: binary hypothesis rejected; Null/NS lead
- **Context:** Critique: binary-outcome account not supported (VM Binary 0.38 vs Bio Binary 1.57); “partially compatible” too kind; Agri Null/NS 14/20 is the better lead.
- **Decision:** Draft_023; Excel Draft_004 (notes cleaned; no process language).
- **Edits:** Binary account of VM density stated as not supported; VM low rate = VM pattern. Null/NS share (Agri 14/20 vs VM 2/20) and Acs2 null-rescue named as clearer suggestive lead. Excel notes match.
- **Status:** active. Working draft = Draft_023.

## 2026-10-03 — Draft_022 + Excel Draft_003: Acs2 rescue-hedging; outcome-type coding; Ethics/Aas9; clustering
- **Context:** Critique: Acs2 dismissed as noise; VM binary hypothesis untested; adviser clustering under KW; Aas9 title not anonymized.
- **Decision:** Draft_022 from Draft_021; CompiledResult Draft_003 with Outcome Type sheet.
- **Edits (thesis):**
  1. Acs2: named as null-result rescue hedging (overclaiming risk), not only formulaic density inflation.
  2. Outcome type coded for all 60 (Binary/Continuous/Mixed/Null/NS/Other); VM Binary 8/20, mean 0.38 hedges; partial support only.
  3. Kruskal-Wallis: independence/clustering caveat next to the p-value.
  4. Ethics: names anonymized; titles in source text redacted where identifying; Aas9 title → [TITLE REDACTED].
- **Excel:** New sheet Outcome Type + cross-tabs.
- **Status:** active. Working draft = Draft_022.

## 2026-10-03 — Draft_021 Methods: full re-code after codebook finalized
- **Context:** User corrected prior assumption. After first-pass coding and rule refinement, the full corpus was re-coded under the final codebook; intra-rater second pass used that same codebook.
- **Decision:** Methods text updated. knowledge.md records the fact.
- **Status:** active.

## 2026-10-03 — Draft_021: Part IV unified; differentiation claim; re-coding admission
- **Context:** Critique: VM paragraph half-converted; Ag/Bio still labeled as profiles; “Disciplinary differentiation is present” too strong; rule-refinement hole (re-checked or not?).
- **Decision:** Draft_021 from Draft_020.
- **Edits:**
  1. Part IV: Ag/Bio/VM profile blocks folded into one short paragraph; VM factive-verb claim moved to labeled hypothesis only.
  2. Conclusions + Part IV summary: “Limited evidence of differentiation, mainly Veterinary Medicine.”
  3. Methods: refinements applied to subsequent coding; earlier abstracts not systematically re-checked against final rules.
- **Note:** If earlier abstracts *were* re-coded, Methods sentence must be corrected.
- **Status:** active. Working draft = Draft_021.

## 2026-10-03 — Draft_020: consistency pass (VM label, cross-refs, potential, Part IV heading)
- **Context:** Critique: Part IV still called VM “assertive reporting”; Scope cross-refs wrong (pilot → Results, Crop/Animal “counts” in sampling table); “learned formula” on potential; Part IV heading overpromised.
- **Decision:** Draft_020 from Draft_019.
- **Edits:**
  1. Part IV heading → “CROSS-DISCIPLINARY CONTRASTS”
  2. VM section → “lower density, cause unknown”; not a measured assertive profile
  3. Scope: pilot comparison → Appendix B; Table 1 = sample sizes not hedge counts
  4. Part I potential: dropped “learned formula”; boundary judgment under Working Test, open to alternative readings
- **Status:** active. Working draft = Draft_020.

## 2026-10-03 — Draft_019: RQ3 question restored to approved wording
- **Context:** User clarified only the RQ3 *discussion* should be reframed, not the question text (approved version stands).
- **Decision:** RQ3 question restored to “Among the hedging devices identified, what rhetorical functions do they serve?” Framework/Part III discussion still treats the 100% EC result as a finding about the scheme under the Working Test.
- **Status:** active.

## 2026-10-03 — Draft_019: panel-critique revisions (RQ3 scheme, pro forma dropped, Part IV shrunk, Scope cleaned)
- **Context:** External “honest opinion” critique. User instructions: (1) single-coder keep as is; (2) acknowledge codebook refined on main corpus, no need to narrate every correction in paper/excel; (3) RQ3 as finding about the scheme; (4) shrink theoretical claims; (5) drop pro forma; (6) soften baseline, finish assertive note, Crop/Animal note; (7) remove results numbers from Scope.
- **Decision:** New Draft_019 from Draft_018.
- **Edits:**
  1. RQ3 reframed: “How does the adapted function scheme classify the retained hedges… under the Working Test?” Framework text aligned.
  2. Methods: pilot established overall scheme; boundary decision rules refined during main-corpus coding and logged.
  3. Pro forma: removed from Definition of Terms; removed three-observation paragraph from Part IV; Conclusions no longer uses “formulaic potential” as construct language. Term count = 0.
  4. Part IV + Conclusions: defensible claim = “VM abstracts in this corpus hedge less; the cause remains unknown.” Rival explanations named, not resolved.
  5. “Sharp departure from expert norms” softened (no matched expert-abstract baseline).
  6. Assertive-forms count clarified as zero-hedge subset only; no comparison claim.
  7. Crop/Animal: “documented separately” replaced with sampling-table note; no separate inferential comparison.
  8. Scope: removed 65 / 41.7% / pilot 75% results leakage; points to Results chapter.
- **Status:** active. Working draft = Draft_019.

## 2026-10-03 — Draft_018 override: RQ3 discussion + RQ4/pro-forma framing
- **Context:** External critique: RQ3 100% EC is near-tautological under Working Test; RQ4 still framed around individual researchers while Limitations concede adviser/institutional effects; pro forma leans on zero-hedge abstracts.
- **Decision:** Override Draft_018 (no Draft_019). Keep RQ3 wording; reframe how 100% EC is discussed. Lightly reframe RQ4 and related passages to “ratified abstracts … at PSAU.” Keep pro forma label; tighten so it does not treat zero-hedge abstracts as evidence of non-calibration.
- **Edits:**
  1. Part III opening: “Under the Working Test… As a direct consequence… all 65 retained tokens were coded EC.”
  2. Conclusions: same Working-Test consequence note for 100% EC.
  3. RQ4: “…in the ratified abstracts of developing researchers at PSAU.”
  4. Part IV intro + Significance + Conclusions disciplinary claim aligned to ratified-abstracts framing.
  5. Pro forma: observation (2) now “under the Working Test”; explicit clause that zero-hedge abstracts do not themselves demonstrate non-calibration.
- **Status:** active. Draft_018 (overridden) is current working draft.

## 2026-10-03 — Draft_018: critique fixes (stats language, Recommendations dupe, catalog-year inclusion, B2 note, pro-forma softener)
- **Context:** External comment flagged approximate-p sensitivity language, duplicated Recommendations paragraph, undefined “completion” vs B2 2018–2019 conduct date, and over-weight of “pro forma” label. Confirmed present in Draft_017.
- **Decision:** Create Draft_018 from Draft_017 with five targeted edits only. No new analysis or count changes.
- **Edits:**
  1. Sensitivity check: removed “(approximately p ≈ .025)”; now states directional pattern only.
  2. Recommendations: deleted the second, near-verbatim “Instruction should also distinguish topic-naming potential…” sentence.
  3. Scope + Inclusion/Exclusion + pilot: inclusion window defined as hard-bound submission year in PSAU library catalog (not research-conduct year); irregular-student lag explained.
  4. B2 abstract: coder note “[Conducted 2018–2019; bound and catalogued 2023 per library records]”.
  5. Pro forma: “learned lexical shell” → “formulaic—a limited set of frames and one function”.
  6. Cosmetic: remaining “p ≈ .033” → “p = .033”.
- **Status:** active. Working draft = Draft_018.

## 2026-10-02 — Draft_013 labeled as FINAL
- **Context:** User uploaded manually-edited version of Draft_012
  ("My Thesis Final - Draft.docx") with minor changes: Tables 3
  and 4 reformatted, "institutions and cohorts" → "institutions
  and groups", codebook and Combined Example paragraphs simplified,
  trailing period removed in two places (one was a typo). Saved as
  Draft_013. User then instructed to fix the "producti" typo
  (restore "production.") and label the result as the finalized
  edit in the repository.
- **Decision:** Draft_013 is the FINAL draft. Git tag
  `final-draft-013` created. `projects.md` Stage field updated to
  reference Draft_013 as the final manuscript draft. Future
  revisions (if any) should create Draft_014+, not overwrite
  Draft_013.
- **Edits applied to Draft_013:**
  1. User's manual edits (Tables 3&4 reformatted, text simplifications)
  2. Typo fix: "producti" → "production." in Appendix C paragraph 510
- **Status:** active. Draft_013 = FINAL.

## 2026-10-02 — Draft_012 comprehensive formatting pass (4 fixes)
- **Context:** User requested: (1) custom BAELS table borders,
  (2) prevent mid-word splitting in tables (lower font size to fit
  instead), (3) remove blank pages, (4) fix title page.
- **Decisions:**
  1. **BAELS borders re-applied** (after briefly reverting to
     TableGrid to match D5 in prior round). All 14 tables now have
     2¼pt top/bottom, ¼pt header divider, no verticals, no insideH.
  2. **Word wrapping fix:** Set `tblLayout=fixed` (prevents autofit
     from shrinking columns and forcing mid-word breaks) +
     `wordWrap=0` on all table cell paragraphs (don't break mid-word;
     wrap at word boundaries instead) + reduced 11pt cell content to
     10pt across all tables for breathing room.
  3. **Blank pages removed:** 17 leading empties after section breaks
     removed. Section breaks already create page breaks; the empties
     were creating top-of-page blank space (1+ inch of empty space
     before INTRODUCTION, METHODOLOGY, etc.).
  4. **Title page fixed:** Reduced 8 top-of-page empty paragraphs to
     2. Title was being pushed ~2.7 inches down from top margin;
     now appears near the top of the page per companion guide p.14
     layout.
- **What was NOT changed:** Title page content structure (title,
  "A Thesis", Presented to..., By, author, date) — already matches
  companion guide p.14 for post-proposal-defense stage. Title
  inverted-triangle format (line 1 longer than line 2) already
  compliant.
- **Conflict note:** D5 spacing pattern (4 empties before major
  headings, applied last round) and "remove blank pages" this round
  are in tension. Resolved by removing the 4 leading empties for
  major headings that follow section breaks (since the section break
  already creates the page break). D5 spacing preserved for sub-
  headings and headings not following section breaks.
- **Status:** active.

## 2026-10-02 — Draft_012 in-place edit (override, no new draft)
- **Context:** User explicitly instructed "don't create new draft,
  override current v12" when asking for blank-page removal and table
  split prevention.
- **Decision:** Override the prior "don't touch old versions" rule
  for Draft_012 specifically. Draft_012 is now treated as the live
  working file — further formatting fixes go into it in place, not as
  Draft_013+.
- **Rationale:** User's call. Drafts 001–011 are still preserved
  (those represent content revisions the user may want to revert to).
  Draft_012 is the formatting-cleanup draft, distinct from the content
  drafts. Treating it as live for formatting iterations keeps the
  draft count from inflating for purely cosmetic changes.
- **Edits applied in this round:**
  1. Removed 30 consecutive empty paragraphs that caused blank pages.
  2. Set `cantSplit=True` on all 64 table rows (prevents row splitting
     across pages).
  3. Set `tableHeader=True` on all 14 first rows (repeats header if a
     table does split across pages).
- **Status:** active. Override rule applies to Draft_012 only. If user
  asks for content changes (not just formatting), revert to creating
  Draft_013+.

## 2026-10-02 — Apply BAELS table format per Thesis Companion p.25
- **Context:** User uploaded `001_ThesisCompanion.pdf` (the BAELS
  Thesis Companion formatting guide by Andrea Mae S. Baltazar) and
  asked to apply appropriate formatting to Draft_011 per the guide.
  Inspection found all other formatting (page setup, margins, fonts,
  heading hierarchy, pagination, double-spacing, section breaks)
  already correct. Only the table format was wrong: all 14 tables
  used `TableGrid` style (¼pt borders everywhere).
- **Decision:** Apply BAELS-prescribed table format to all 14 tables:
  - Top border: 2¼pt (sz=18 in 1/8 pt units)
  - Bottom border: 2¼pt
  - Header divider (inside, below first row): ¼pt
  - No vertical borders (left, right, insideV)
  - No other horizontal borders (insideH)
  Per Thesis Companion p.25: "The top and bottom border lines of the
  table have 2 ¼ pts. The only inside line found at the header part
  is ¼ pt."
- **Saved as:** `003_ThesisProposal_Draft_012.docx` (new file, per
  user's prior instruction not to overwrite old versions).
- **What was NOT touched:** Title page "A Thesis" text — the
  companion guide p.14 shows "A Thesis [Proposal]" with a side note
  that "Proposal" should be removed at final defense. The brackets
  are ambiguous (could be instructional or could be literal text).
  User is at proposal stage (defense Oct 2026 per projects.md), so
  strictly it may need "A Thesis Proposal" — but this is content,
  not pure formatting, and the spec is ambiguous. Flagged in main
  reply; not changed unilaterally.
- **Companion guide preservation:** `001_ThesisCompanion.pdf` copied
  to `thesis/` directory and committed to repo. Future sessions now
  have it without needing re-upload.
- **Status:** active.

## 2026-10-02: Draft_007, narrative rewrite from Draft_005
- **Context:** User asked for a full rewrite applying preferences.md, keeping only the title, research questions and corpus verbatim, with redundancies fixed, as a new draft based on Draft_005.
- **Decision:** Draft_007 keeps verbatim the title page, RQ1 to RQ4, and the whole Research Corpus section (text, Table 1, inclusion, exclusion, ethics). Everything from Introduction to Recommendations is rewritten. Data tables, references, appendices and the coded corpus are untouched. Sampling detail now lives only under Research Corpus, and the coding stages only under Research Framework.
- **Why:** The verbatim corpus section made it the single home for sampling details, so Scope, Research Process and Definitions point to it instead of repeating it.
- **Status:** active. Draft_006 and earlier retained.

## 2026-10-02: Script verdicts over model claims
- **Decision:** `doctor.sh` reports health through its exit code, run at
  session start and before the final push. Scanner reports show only 4
  characters of a match plus its length.
- **Why:** An agent saying "all clean" proves nothing, and the protocol
  already admits an LLM can skip steps. A script can't be talked out of a
  FAIL. CI logs on a public repo are public, so a 24-character prefix of a
  real token was too much to print.

## 2026-10-02: Front-door files and a paste pack
- **Decision:** `AGENTS.md` and `CLAUDE.md` point desktop agents at
  `context.md`. `paste_pack.sh` makes a size-capped bundle for chats with no
  sandbox and names what it omitted.
- **Why:** Desktop agents look for these file names on their own, so nobody
  has to paste the opening prompt. The pack covers the case where the repo
  can't be reached. The two front-door files are identical copies because I
  couldn't confirm that every tool follows an include from one to the other.
- **Rejected:** One file importing the other.

## 2026-10-02: Session end, duplicate check, forgetting
- **Decision:** `context.md` gains an end-of-session checklist, a
  search-before-save rule, an `applied lesson:` notice, and a forgetting
  rule.
- **Why:** The protocol covered starting and working but not ending, so
  durable items stayed buried in transcripts. Searching first keeps one entry
  per fact. The notice makes lessons auditable. Deletion in git never erases
  history, so the user should hear that before they rely on it.


## 2026-10-01: Zero-dependency search ahead of embeddings
- **Decision:** `scripts/search.sh` is the default retrieval tool: literal,
  case-insensitive, capped, lessons first, and it states how many results
  are hidden and says plainly when there are none.
- **Why:** The embeddings tool needs torch and a model download, which
  sandboxed web agents often can't run. A search that fails silently is
  worse than none, so a zero result and a truncated result are both made
  explicit. Matching is literal because the caller is usually an agent
  passing free text. Borrowed from create-ai-memory's search design.
- **Rejected:** Fuzzy matching and regex (wrong answers on free text).
  Making embeddings the default.

## 2026-10-01: lessons.md, separate from decisions
- **Decision:** Mistakes and their fixes live in `lessons.md`, one entry each
  with a "Doesn't apply when" line. Lessons are never archived.
- **Why:** A decision records a choice. A lesson records a failure and its
  fix, and it is what you need months later when the same problem returns.
  Archiving by age would delete exactly those. The "Doesn't apply when" line
  keeps lessons from hardening into rigid rules. Pattern taken from gitmem
  and create-ai-memory.
- **Rejected:** Folding lessons into `decisions.md`, where they'd be archived
  with it.


## 2026-09-08 — Sync preferences.md from ai-mem2 repo
- **Context:** User maintains preferences.md in two repos:
  `ckmanuel/ai-mem2` (the canonical source) and `ckmanuel/thesis-memory`
  (this repo, where it's used for thesis-session context). User made
  revisions to ai-mem2's preferences.md in three commits:
  - 309683b — Add "don't be more specific than the question warrants"
  - 5df3df9 — Broaden to cover constructed content too
  - 6ff6d63 — Replace with lean updated directive (final form)
- **Decision:** Mirror ai-mem2 preferences.md in thesis-memory.
  ai-mem2 is canonical for preferences.md. When the user revises
  preferences in ai-mem2, sync the changes here.
- **Changes synced:** Four discrete edits:
  1. "Clear, common language." → "Use clear, common language."
  2. "Favor active voice; allow passive..." → "Favor active voice but
     allow passive..." (semicolon → "but")
  3. New bullet in "Things to watch" on excessive, unearned
     specificity (covers both answering questions and writing content)
  4. New bullet in "What the Assistant Should Avoid" on same theme;
     reformatted "what's next?" bullet (removed bold lead-in)
- **Rationale:** User has multiple memory repos (ai-mem2 for general
  context, thesis-memory for thesis-specific work). preferences.md
  should be identical across both to avoid drift. ai-mem2 is the
  canonical source because that's where the user actively edits it.
- **Status:** active.

## 2026-09-10 — Draft_003 writing-voice revision per preferences.md
- **Context:** User requested: apply preference and revise the thesis
  accordingly, then push as a new draft.
- **Decision:** Created and pushed `003_ThesisProposal_Draft_003.docx`.
  Targeted voice pass on Background of the Study and Conclusions
  (and a few literature-review transitions): shorter sentences, more
  active constructions, cut decorative or stacked phrasing, kept
  meaning and citations intact. Prior drafts (001, 002) retained in
  working tree.
- **Rationale:** Align authorial prose with the preferred voice
  (clear, direct, varied, no AI-polish) while remaining appropriate
  for a BA thesis.
- **Status:** active

## 2026-09-10 — Draft_002 claim consistency + Table 6 softening (keep Draft_001)
- **Context:** User requested the necessary adjustments for submission
  readiness (claim consistency, Table 6 / Recommendations alignment
  with exploratory framing), then authorized push with explicit
  instruction: do not delete the older version in git.
- **Decision:** Created and pushed `003_ThesisProposal_Draft_002.docx`
  with targeted edits only:
  1. “valid and significant indicator” → “valid indicator”
  2. Recommendations lead-in softened
  3. Table 6 intro rewritten as provisional / exploratory guidance
  4. Table headers: Common Issue → Observed Pattern; Revision Target
     → Possible Focus
  5. Cell language softened
  `Draft_001` retained in the working tree alongside `Draft_002`
  (overrides the normal “remove previous Draft on push” rule for
  this instance only, per user instruction).
- **Rationale:** Keeps exploratory baseline stance consistent.
  User override on version retention honored.
- **Status:** active

## 2026-09-08 — Thesis file versioning convention
- **Context:** Thesis revisions will accumulate over time. Need a
  naming convention that distinguishes the original pre-edit version
  from subsequent draft revisions, and that supports future versions
  without colliding with old ones.
- **Decision:** Two file classes in `thesis/`:
  1. **Preedit** — the original uploaded file, preserved unchanged.
     One Preedit per uploaded file (docx, xlsx, etc.). Set once,
     never modified, never deleted. Even if the file is not revised
     in a given session, its Preedit remains in the working tree
     as the canonical reference for the original upload.
     Current Preedit files:
     `003_ThesisProposal_Preedit.docx`,
     `007_CompiledResult_Preedit.xlsx`.
  2. **Draft_###** — the current working revision of a file that
     has actually been revised in this session. Three-digit
     zero-padded counter. Only files that were touched in a
     session get a Draft copy. Current Draft files:
     `003_ThesisProposal_Draft_001.docx`.
- **Push rule (corrected 2026-09-08 after user feedback):**
  - Every uploaded file gets a Preedit, always. Preedit is never
    removed, even if the file is never revised.
  - Only files that were actually revised get a Draft_NNN copy.
    If a file was not touched in this session (e.g., the xlsx
    coding sheet when only the docx was edited), do NOT create a
    Draft copy of it. Adding a byte-identical "Draft_001" alongside
    the Preedit is the redundant pattern to avoid.
  - The first backup push in session 1 already preserved the
    original uploads in git history under their original
    `(N)`-suffixed filenames (e.g., `007_CompiledResult (4).xlsx`).
    The Preedit copies in the working tree are the canonical
    reference, not the git history artifacts.
- **Version bump rule:** when a new revision is pushed, the previous
  `Draft_NNN` is removed and replaced by `Draft_(NNN+1)`. We do NOT
  accumulate `Draft_001.docx`, `Draft_002.docx`, etc. in the same
  commit — git history serves that role. Only the current draft
  lives in the working tree.
  - Exception: if the user explicitly asks to keep an old draft,
    preserve it with a date suffix, e.g. `Draft_001_2026-09-15.docx`.
- **Counter starts at:** 001 (current draft, applied 2026-09-08).
- **Rationale:** Avoids filename proliferation. Each push has
  exactly one Preedit per uploaded file (always) plus one current
  Draft per file that was actually revised (when applicable).
  Git history provides the diff trail between drafts. Three-digit
  padding keeps lexical sort correct up to 999 versions.
- **Status:** active.

## 2026-09-08 — Thesis binaries backed up via force-add (one-off)
- **Context:** User uploaded thesis draft files (`003_ThesisProposal
  (4).docx` ~349 KB and `007_CompiledResult (4).xlsx` ~35 KB) and
  asked to push them to the memory repo for backup.
- **Decision:** Force-add the binaries with `git add -f`, overriding
  the default `.gitignore` block on `*.docx` / `*.xlsx`. One-off,
  acceptable for a single snapshot of important work.
- **Rationale:** The README explicitly warns that binary pushes bloat
  git history and slow future clones. For a one-time backup of ~384 KB
  total, the cost is negligible. The user explicitly asked for backup,
  and the work is significant (thesis).
- **Forward guidance:** For repeated thesis revisions, prefer Git LFS
  or a separate dedicated backup repo. Don't make force-add a habit.
- **Status:** active

## 2026-09-08 — Retrieval tools: prune, index, embeddings
- **Context:** As `chat_history/` grows, finding what was said in past
  sessions becomes a grep problem. Three layers added to address
  different scales of corpus.
- **Decision:** Three scripts, each solving a different retrieval
  problem:
  1. `scripts/prune_chat_history.sh` — moves transcripts older than N
     days (default 180) to `archive/chat-history-<date>/`. Reduces
     active corpus size. Doesn't solve semantic search; solves the
     "500 transcripts" problem by reducing 500 to 50.
  2. `scripts/update_index.py` — generates `chat_history/INDEX.md`
     with one-line summary per session (date, model, session_id,
     first user message). Grep this file instead of grepping every
     transcript. Pure Python, no deps.
  3. `scripts/embeddings.py` — builds SQLite DB of exchange embeddings
     at `~/.cache/ai-memory-embeddings.db` (outside the repo,
     regeneratable). Uses `sentence-transformers` with
     `all-MiniLM-L6-v2` model (~80MB). Provides `build`, `status`,
     `search` subcommands. Optional dep documented in
     `scripts/requirements.txt`.
- **Why three layers, not one:** each layer addresses a different
  scale. Pruning handles 500+ transcripts by reducing the active
  corpus. Index handles 50+ transcripts by giving grep a smaller
  target. Embeddings handle semantic search that grep can't do.
  User adopts each layer as the corpus grows, not all at once.
- **Embeddings DB outside repo:** derived artifact, regeneratable
  from transcripts, user-specific. Doesn't pollute git history.
  If DB corrupts, delete and rebuild.
- **Status:** active — scripts implemented and tested on empty repo.
  Embeddings not tested end-to-end in this workspace (sentence-
  transformers requires torch which exceeds workspace disk). Script
  handles missing dependency with clear install instructions.


## 2026-10-02 — Draft_008 accuracy fixes on Draft_006 base (ignore Draft_007)
- **Context:** User confirmed Draft_006 and Draft_007 are parallel rewrites from Draft_005. Requested fixes from the accuracy-flag list be applied to Draft_006 (not Draft_007) and pushed as Draft_008.
- **Decision:** Created `003_ThesisProposal_Draft_008.docx` from Draft_006 with five confirmed corrections + soft timeline adjustment:
  1. Zero-hedge comparison: “less than a third” → “40% in Agriculture and 35% in Biology”
  2. Booster average: 3.4 → approximately 3.1 (88÷28)
  3. Scope statement reconciled to allow the limited booster count on the 28 zero-hedge abstracts while stating full booster analysis was not undertaken
  4. Landis & Koch (1977) added to References (was cited for κ interpretation but missing)
  5. Pilot sample size prose aligned to table: “3 to 5” / “3–5” → “4”
  6. Timeline: “approximately 5 months” → “approximately 5.5 months (24 weeks)”
  Appendix A vs C overlap left unchanged (editorial, not factual error). Draft_007 retained as parallel rewrite.
- **Rationale:** User explicitly designated Draft_006 as the reference base. All five hard flags were verified against Draft_005 numbers and accepted.
- **Status:** active

## 2026-10-02 — Draft_008 Verb Tense Matrix alignment (override, no Draft_009)
- **Context:** User supplied Verb Tense Matrix and asked for tense check of Draft_008. Initially pushed as Draft_009; user instructed to remove Draft_009 and override Draft_008 instead.
- **Decision:** Draft_008 overwritten in place with three minor tense cleanups. Draft_009 deleted.
  1. Timeline: “Total estimated timeframe” → “Total timeframe”
  2. Ethical retention: “are retained / are permanently deleted” → “will be retained / will be permanently deleted”
  3. Disciplinary classification rule: “follows” → “followed” (two places)
  Draft_008 remains the current version. No residual proposal-stage “will” in author methodology.
- **Rationale:** User preference for in-place override rather than a new draft number for small tense polish.
- **Status:** active

## 2026-10-02 — Draft_009: merge Appendices A+C, rewrite non-corpus appendices
- **Context:** User chose option 2 (latter): put one-page quick-reference at top of the full codebook and treat the whole as one appendix. Also requested rewrite of appendices (excluding the coded corpus) in preferred voice, as new draft (not override).
- **Decision:** Created `003_ThesisProposal_Draft_009.docx`:
  - Old A (short coding key) + old C (full codebook) merged into **Appendix A: Hedging Codebook**, opening with a one-page Quick-Reference then the full protocol, rewritten in preferred voice.
  - Old B (Pilot) rewritten framing/observation; four sample abstracts and counts retained as data → still **Appendix B**.
  - Old D (Coded Corpus with Highlights) renumbered to **Appendix C**; content left intact.
  - Body references to “Appendix A” for decision rules remain valid (now point at the merged codebook).
- **Rationale:** Removes redundancy, keeps the operational codebook as the single source of truth, applies voice preference consistently to the methodological appendices.
- **Status:** active


## 2026-10-02 — Draft_009 appendix merge reverted (format restore)
- **Context:** Appendix A+C merge + voice rewrite destroyed Georgia formatting, centered titles, and codebook tables. User flagged the result as butchered.
- **Decision:** Draft_009 reset to Draft_008 content (accuracy + tense fixes preserved; original appendix formatting restored). Physical merge of A+C deferred until it can be done without stripping styles/tables.
- **Status:** active

## 2026-10-02 — Draft_009: D8 body + D5 appendices
- **Context:** User rejected butchered appendix rewrite. Requested Draft_005 appendices (original formatting) combined with Draft_008 main body (accuracy + tense fixes).
- **Decision:** Built Draft_009 by splicing Draft_008 body (everything before appendices) with Draft_005 appendix block (APPENDICES through end). Georgia titles, codebook tables, and corpus highlights restored from D5. Body retains D8 fixes (zero-hedge rates, booster avg, scope wording, Landis ref, pilot n=4, timeline 5.5 months, tense cleanups).
- **Status:** active


## 2026-10-02 — Draft_009 appendix changes applied (merge A+C, rewrite framing)
- **Context:** User asked to apply appendix changes on the D8-body + D5-appendices base.
- **Decision:** Draft_009 now has:
  - **Appendix A: Hedging Codebook** — one-page Quick-Reference (preferred voice) + full codebook from D5 (tables/Georgia preserved; PURPOSE opening rewritten).
  - **Appendix B: Pilot** — intro and closing observation rewritten; four samples kept as data.
  - **Appendix C: Coded Corpus** — old D, content/highlights untouched.
  - Main body still D8 (accuracy + tense fixes).
- **Status:** active


## 2026-10-02 — Remove Table 6 (adviser checklist)
- **Context:** Table 6 told Vet Med students to insert 1–2 hedges, contradicting the thesis's account of binary results and encouraging pro forma hedging.
- **Decision:** Removed Table 6 in Draft_010. Reframed recommendations: feedback targets overclaiming in implications, not hedge quotas; binary/measured results may need no hedge.
- **Status:** active


## 2026-10-02 — Cut Chapter 3–4 redundancies (Draft_011)
- **Context:** User confirmed repeated interpretation across Results Parts II–IV and Conclusions.
- **Decision:** Draft_011 keeps counts/tests in Parts I–II, EC and result/implication in Part III, discipline labels in Part IV with pointers back, shortened Conclusions. Potential concordance and pro forma notes tightened. ~19% fewer words in Results+Conclusions block.
- **Status:** active

## 2026-10-05 — Draft_040: remove em dashes, keep en dashes and hyphens
- **Context:** User asked for a new draft with no em dashes. Also reported words that looked joined after en dashes were removed.
- **Decision:** Created Draft_040 from Draft_039. All em dashes (U+2014) rephrased with periods, commas, or parentheses. En dashes (U+2013) for ranges (Acs1–Acs10, 2023–2025, page spans) and hyphens in compounds (Kruskal-Wallis, chi-square, adviser-enforced) left intact. No fused-word damage found between Draft_038 and Draft_039. Draft_038 removed under keep-2 policy. Working draft = Draft_040.
- **Status:** active. Working draft = Draft_040.

## 2026-10-06 — Draft_040: root-grouped frequency tallies
- **Context:** User asked why suggest/suggests/suggesting were listed separately in the Results tally and requested root-compiled presentation.
- **Decision:** Overwrite Draft_040. Part I frequency sentence now groups lexical forms by root: suggest/suggests/suggesting (13), imply/implies/implying (3), indicating (2). Potential stays at 19 (lexical only). Potentially remains under adverbial hedges (3) and is not merged with potential. Modal verbs stay separate roots (can, could, may, might). Part III wording aligned to suggest/suggests/suggesting. Coding sheet unchanged (still one row per surface token).
- **Status:** active. Working draft = Draft_040.

## 2026-10-06 — Draft_041: Table 3 Hedge Token Inventory by Form
- **Context:** User asked to list all hedges in the tally (discussion or table) so form counts can be checked. Requested a new draft if a table is added.
- **Decision:** Draft_041 from Draft_040. New **Table 3: Hedge Token Inventory by Form** after the Part I frequency paragraph. Lists every surface form with Layer 1 type, count, and % of 65. Former Tables 3–6 renumbered to 4–7 (captions and body refs). Coding sheet unchanged. Draft_039 removed under keep-two policy (040 previous, 041 current).
- **Status:** active. Working draft = Draft_041.

## 2026-10-06 — Draft_041: fix Research Process step b bold spill
- **Context:** User reported step b under Research Process spilled bold across the whole paragraph.
- **Decision:** Overwrite Draft_041. Step b label only is bold ("b. Corpus Construction. "). Body unbolded to match steps a, c, d, e. Scanned Methods for other full-paragraph bold body runs. None found outside intentional appendix headers and Significance lead-ins.
- **Status:** active. Working draft = Draft_041.

## 2026-10-06 — Draft_041: keep Table 3 caption with table body
- **Context:** User reported only one table had label/heading separated from the table body across pages.
- **Decision:** Overwrite Draft_041. Page break before Table 3 caption. Keep-with-next on caption and title. Inventory table rows cantSplit + header repeat.
- **Status:** active. Working draft = Draft_041.

## 2026-10-06 — Draft_042: expand outcome-type definitions in Part IV
- **Context:** User asked whether Table 7 categories were unexplained or ambiguous in the discussion, requested the fuller explanation in text, a new draft, and no deletion of older drafts for now.
- **Decision:** Draft_042 from Draft_041. Part IV paragraph at Table 7 now defines each category in plain sentences (Binary, Continuous, Mixed, Null/NS, Other), states coding is from the abstract’s results language, and lists Table 7 totals. Analytic claims on VM Binary vs Biology Binary and Agriculture Null/NS/Acs2 retained. Keep-two deletion policy suspended for this stretch. Working draft = Draft_042.
- **Status:** active. Working draft = Draft_042.

## 2026-10-06 — Draft_042: plain-style outcome-type definitions
- **Context:** User found the Draft_042 thesis wording harder than the chat explanation and asked to keep the chat-style clarity.
- **Decision:** Overwrite Draft_042. Part IV defines each Table 7 category with counts and concrete examples in short sentences matching the chat explanation. Analytic claims retained.
- **Status:** active. Working draft = Draft_042.

## 2026-10-06 — Excel: add Table 7 cross-tab and outcome-type definitions
- **Context:** User asked to add “that table” to the Excel after the Part IV outcome-type explanation work.
- **Decision:** Overwrite `007_CompiledResult_Draft_005.xlsx`. Added Outcome Type by Discipline (Table 7) and Outcome Type Definitions (plain meanings + counts) on both Summary and Outcome Type sheets. Counts verified against coding rows (60 abstracts).
- **Status:** active.
