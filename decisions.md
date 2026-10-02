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

## 2026-10-02 — Draft_009 Verb Tense Matrix alignment on Draft_008
- **Context:** User supplied Verb Tense Matrix (Proposal → Final) and asked for tense check/correction of Draft_008.
- **Decision:** Draft_008 was already largely correct for final-defense tenses (methodology past, results past, recommendations present+should, table pointers present). Three minor cleanups applied and pushed as Draft_009:
  1. Timeline: “Total estimated timeframe” → “Total timeframe”
  2. Ethical retention: “are retained / are permanently deleted” → “will be retained / will be permanently deleted” (past for storage action already present; future for retention plan)
  3. Disciplinary classification rule: “follows” → “followed” (two places)
  No leftover proposal “will” in author methodology; corpus examples left intact.
- **Rationale:** Matrix final-defense column. Standing institutional facts remain present; procedure steps past; retention policy future.
- **Status:** active
