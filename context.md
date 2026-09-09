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
- Session `auto-1788876026-5ea42e` (Grok) continued 2026-09-10.
- Thesis: `Draft_003` created and pushed (writing-voice revision per
  preferences.md). Draft_001 and Draft_002 retained. Preedit originals
  preserved.
- See `projects.md` for file inventory, `decisions.md` for
  versioning convention.

## Open Threads
- `preferences.md` still has unfilled sections: Tooling & Environment,
  Document & Output Preferences, Coding Style. Capture these as they
  emerge.
- The PAT cannot create new repos (no Administration scope). Not a
  blocker since we're staying in one repo.
- **Recurring pattern: PAT pasted in plaintext at session start.**
  Now observed in at least six sessions (claude-app-mobile-9f3a2c,
  the first 2026-09-08 auto-* session, the 2026-09-08 Claude mobile-app
  session, the 2026-09-08 auto-1788872698-9bc8ca Claude.ai session,
  the 2026-09-08 auto-1788872764-186d49 Claude.ai session, and this
  2026-09-08 auto-1788876026-5ea42e Grok session). The opening prompt
  template supports `$GH_PAT` env var reference, but the user keeps
  pasting the literal token instead. Each occurrence is a live
  credential exposed in chat logs. Recommend rotation after the
  session. Consider making the env-var option the only documented
  path in the README opening prompt, since the plaintext option keeps
  getting used despite the alternative.

## Recently Completed
_(Capped at 5 entries. Older items live in `decisions.md` and the
verbatim transcript at `chat_history/`.)_

- 2026-09-10 — Pushed `003_ThesisProposal_Draft_003.docx` (writing-
  voice pass per preferences.md: tighter, more direct prose in
  Background and Conclusions). Prior drafts retained.
- 2026-09-10 — Pushed `003_ThesisProposal_Draft_002.docx` (claim
  consistency + Table 6 / Recommendations softening). Draft_001 kept
  in working tree per user request.
- 2026-09-08 — Synced preferences.md from ai-mem2 repo. Four edits
  applied; ai-mem2 designated canonical source for preferences.md.
  See `decisions.md`.
- 2026-09-08 — Session `auto-1788876026-5ea42e` (Grok) opened.
  Repo cloned, token stripped from remote URL, credential helper
  set via $GH_PAT, hooks installed, transcript started. PAT
  redaction count incremented to six.
- 2026-09-08 — Session `auto-1788872764-186d49` opened (immediately
  after `auto-1788872698-9bc8ca`; same state, no work in between).
  PAT redaction count incremented to five.
- 2026-09-08 — Session `auto-1788872698-9bc8ca` opened. Token stripped
  from `.git/config`; ephemeral credential helper installed (reads
  from `$GH_PAT` env var). Pre-commit hook reinstalled on fresh clone.
  Context and Open Threads updated.
- 2026-09-08 — Restored `007_CompiledResult_Preedit.xlsx` after
  incorrect removal. Push rule in `decisions.md` corrected:
  Preedit (original) is always preserved for every uploaded file;
  only Draft copies are created when a file is actually revised.

## Blockers
_None._
