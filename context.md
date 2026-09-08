# Current Context

Read this file first after cloning.

## FIRST ACTION AT SESSION START

```sh
./scripts/new_session.sh [session_id] [YYYY-MM-DD] [model]
```

All args optional. Creates `chat_history/<model>/<session_id>-<date>.md`
with the right header. Don't proceed until this is done.

If your session was idle and another session may have committed, run
`GH_PAT=$GH_PAT ./scripts/sync_before_work.sh` first to pull and see
what changed.

## CRITICAL: Append user message to transcript IMMEDIATELY

**Read `TRANSCRIPT_REMINDER.md` if you haven't already.** It's the
persistent failsafe for this step — survives context truncation.

When you receive a user message, append it to the transcript file
**before** you start working on the response. Don't wait until the
end. If you skip this and the session ends or context truncates, the
exchange is lost forever.

Two ways to do this:

**Option A — use begin_exchange.sh (recommended):**

```sh
echo "the user's message" | ./scripts/begin_exchange.sh <trace_id>
```

Appends a placeholder entry with the user message and an `(in progress...)`
marker for your reply. Replace the marker with your actual reply when
done. If you forget, the transcript shows an incomplete exchange —
visible failure that the next session can backfill.

**Option B — append manually:**

Append to `chat_history/<model>/<session_id>-<date>.md`:

```
#### Exchange N — trace <trace_id>

**User:**

> <user message verbatim, redact any PAT>

**Assistant:**

> <your reply, appended after you finish>
```

Either way: the user half must be captured BEFORE you start working.
The assistant half can be filled in after.

## Why this matters

Memory file changes (preferences.md, decisions.md, knowledge.md,
context.md, projects.md, README.md) without a transcript update will
be blocked by the pre-commit hook (`scripts/pre_commit_transcript_check.py`).
Bypass with `git commit --no-verify` only for genuinely conversation-
independent commits (README typos, script refactors, CI updates).

CI also warns on push when memory files change without a transcript
update. Doesn't block, but makes the failure visible.

## Current Focus
- Thesis revisions in progress. Current draft: `Draft_001` (8 critique-
  driven edits applied 2026-09-08). Preedit preserved separately. See
  `projects.md` for file inventory, `decisions.md` for versioning
  convention.
- Awaiting user's next instruction (further edits? push? new task?).

## Open Threads
- `preferences.md` still has unfilled sections: Tooling & Environment,
  Document & Output Preferences, Coding Style. Capture these as they
  emerge.
- The PAT cannot create new repos (no Administration scope). Not a
  blocker since we're staying in one repo.
- **Recurring pattern: PAT pasted in plaintext at session start.**
  Now observed in at least three sessions (claude-app-mobile-9f3a2c,
  the 2026-09-08 auto-* session, and this 2026-09-08 Claude mobile-app
  session). The opening prompt template supports `$GH_PAT` env var
  reference, but the user keeps pasting the literal token instead.
  Each occurrence is a live credential exposed in chat logs.
  Recommend rotation after the session. Consider making the env-var
  option the only documented path in the README opening prompt, since
  the plaintext option keeps getting used despite the alternative.
- **Recommendations section in thesis may need revisiting.** Once
  findings were downgraded to exploratory (Draft_001), the
  discipline-specific revision checklist in Table 6 is built on the
  typology that was just softened. Flag for user; revise in Draft_002
  if user requests.

## Recently Completed
_(Capped at 5 entries. Older items live in `decisions.md` and the
verbatim transcript at `chat_history/`.)_

- 2026-09-08 — Restored `007_CompiledResult_Preedit.xlsx` after
  incorrect removal. Push rule in `decisions.md` corrected:
  Preedit (original) is always preserved for every uploaded file;
  only Draft copies are created when a file is actually revised.
- 2026-09-08 — Removed redundant `007_CompiledResult_Draft_001.xlsx`
  from `thesis/` (byte-identical to Preedit; no revision made).
- 2026-09-08 — Renamed thesis files to `_Preedit` / `_Draft_001`
  convention. Versioning scheme logged in `decisions.md`. Updated
  `projects.md` and `context.md`.
- 2026-09-08 — Applied 8 critique-driven edits to thesis docx.
  Edits address stats underpowered vs typology claims, single-coder
  reliability on functional findings, "pro forma hedging" construct
  overreach, and missing expert-abstract comparison corpus.
- 2026-09-08 — Thesis backup pushed. Two files force-added to
  `thesis/`: proposal draft (`.docx` ~349 KB) and compiled results
  (`.xlsx` ~35 KB). Project added to `projects.md`.
- 2026-09-08 — Fixed `begin_exchange.sh` "Illegal number: 0" bug.
  Root cause: `grep -c` prints "0" and exits 1 on zero matches; the
  `|| echo 0` fallback fired anyway and duplicated the output to
  "0\n0", breaking arithmetic. Fixed with `|| true` + `${EXISTING:-0}`.
  Verified against a clean fresh-transcript case.
- 2026-09-08 — Transcript enforcement: pre_commit_transcript_check.py
  blocks commits when memory files change without transcript update.
  begin_exchange.sh appends placeholder exchange entry. CI warning
  tightened. context.md workflow updated to append user message at
  start of response. install_hooks.sh now calls both scanners.
  Implemented on both repos.
- 2026-09-08 — Critique round 4 hardening: prune uses git commit date,
  embeddings warns on non-conforming transcripts, PATH false-positive
  regex fixed, update_index uses first user + last assistant, MIT
  LICENSE added, RETRIEVAL.md added, 16-test suite, CI INDEX.md
  staleness check, README "Files outside the repo" section.
- 2026-09-08 — Retrieval tools: prune_chat_history.sh, update_index.py,
  embeddings.py. Tested on 3 transcripts. INDEX.md generated.
- 2026-09-08 — Clean-slate fork `ckmanuel/ai-mem2` set up.

## Blockers
_None._
