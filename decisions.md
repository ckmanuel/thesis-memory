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

## 2026-09-08 — Thesis file versioning convention
- **Context:** Thesis revisions will accumulate over time. Need a
  naming convention that distinguishes the original pre-edit version
  from subsequent draft revisions, and that supports future versions
  without colliding with old ones.
- **Decision:** Two file classes in `thesis/`:
  1. **Preedit** — the original uploaded file, preserved unchanged:
     `003_ThesisProposal_Preedit.docx`. Set once, never modified.
  2. **Draft_###** — the current working revision:
     `003_ThesisProposal_Draft_001.docx`. Three-digit zero-padded
     counter.
- **Version bump rule:** when a new revision is pushed, the previous
  `Draft_NNN` is removed and replaced by `Draft_(NNN+1)`. We do NOT
  accumulate `Draft_001.docx`, `Draft_002.docx`, etc. in the same
  commit — git history serves that role. Only the current draft
  lives in the working tree.
  - Exception: if the user explicitly asks to keep an old draft,
    preserve it with a date suffix, e.g. `Draft_001_2026-09-15.docx`.
- **Counter starts at:** 001 (current draft, applied 2026-09-08).
- **Push rule (revised 2026-09-08 after user feedback):** Only push
  files that have been revised. If a file was not touched in this
  session (e.g., the xlsx coding sheet when only the docx was
  edited), do NOT push a Preedit or Draft copy of it. The original
  is already preserved in git history from the first session's
  backup push. Adding byte-identical Preedit + Draft copies to the
  working tree just bloats the repo without adding signal.
- **Rationale:** Avoids filename proliferation. Each push has
  exactly one preedit + one current draft per file that was
  actually revised. Git history provides the diff trail between
  drafts and preserves untouched files from the initial backup.
  Three-digit padding keeps lexical sort correct up to 999 versions.
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

