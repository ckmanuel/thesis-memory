# Current Context

Read this file first after cloning.

## FIRST ACTION AT SESSION START

```sh
./scripts/new_session.sh [session_id] [YYYY-MM-DD] [model]
```

All args optional. Creates `chat_history/<model>/<session_id>-<date>.md`
with the right header. Don't proceed until this is done.

Then run `./scripts/doctor.sh` and fix any FAIL line before going on. Then
read `preferences.md` and `decisions.md`. Skim `knowledge.md` and
`projects.md` if the task touches them. If the session has been idle and
another session may have committed, run `GH_PAT=$GH_PAT ./scripts/sync_before_work.sh`
before editing.

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

Before adding a lesson, fact, or decision, run `./scripts/search.sh <one
distinctive word>` and update the existing entry if there is one. Run it
also before solving a problem that feels familiar. When you use a saved
lesson, say so in your reply: `applied lesson: <title>`. Other retrieval
tools are described in `RETRIEVAL.md`.

## At session end

1. Promote anything durable from this session: mistakes and fixes to
   `lessons.md`, choices to `decisions.md`, facts to `knowledge.md`.
2. Refresh Current focus and Open threads below. Include what was tried and
   failed, so the next session doesn't repeat it.
3. Run `./scripts/doctor.sh`, fix any FAIL, then commit and push.

## Forgetting

To forget something, edit or delete the entry (or the transcript file) and
commit. Be clear with the user that git history still holds the old text,
and so does any fork or clone made earlier. If the text was a secret, revoke
or rotate it first. Rewriting history is a last resort and doesn't reach
copies already made.

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
  Now observed in at least ten sessions (prior nine plus the
  2026-10-03 auto-1791000856-bb7588 Grok session). The opening prompt
  template supports `$GH_PAT` env var reference, but the user keeps
  pasting the literal token instead. Each occurrence is a live
  credential exposed in chat logs. Recommend rotation after the
  session. Consider making the env-var option the only documented
  path in the README opening prompt, since the plaintext option keeps
  getting used despite the alternative.

- **Draft_013 review (2026-10-02, Claude) — unresolved, no new draft made.**
  Missing from References: Lopez et al. (2025), cited twice. Participant
  codes typed `Acs1–A10`/`Aas1–A10` (should be Acs1–Acs10/Aas1–Aas10).
  Khunasathitchai ref: rEFLections vs IJRISS DOI mismatch, unverified.
  Sampling start "random" vs "around the middle". Scope: dangling pilot
  75% sentence. Kappa rests on 6 abstracts. 100% EC is partly built into
  the Working Test. Conclusions state Agri > Bio order without the Acs2
  caveat. Booster count includes "highest"/"observed". Sampling design
  repeated 3x; Recommendations repeat. Stats recomputed OK.

## Recently Completed
- 2026-10-03 — Created Draft_018 from Draft_017 (Grok session). Fixes from external critique: (1) dropped approximate-p claim in sensitivity check (now reports directional pattern only); (2) removed duplicated “distinguish topic-naming potential…” sentence in Recommendations; (3) operationalized inclusion window as hard-bound / library-catalog year in Scope, Inclusion Criteria, Exclusion Criteria, and pilot note; (4) added coder note on B2 “[Conducted 2018–2019; bound and catalogued 2023 per library records]”; (5) softened pro-forma “learned lexical shell” phrasing. Standardized remaining p ≈ .033 to p = .033.
- 2026-10-03 — Session Grok: Confirmed Combined Example vs Pilot/main-corpus inconsistency was isolated to the illustrative example only. Applied silent corrections in Draft_015: Combined Example now marks conclusion-position “potential” as EC (aligned with final rule, Pilot Sample 2, and all 14 main-corpus decisions); discipline codes Acs1–Acs10 / Aas1–Aas10 fixed. Excel versioned as 007_CompiledResult_Draft_001.xlsx (no numeric change). No mention of the corrections in the paper text.


_(Capped at 5 entries. Older items live in `decisions.md` and the
verbatim transcript at `chat_history/`.)_

- 2026-10-03 — Session `auto-1791000856-bb7588` (Grok) opened: repo
  cloned to /tmp (fuse issues on artifacts path), token stripped from
  remote, hooks installed, doctor passing. Transcript started. PAT
  pasted in plaintext again (redacted); rotation recommended. User
  asked for help finalizing thesis; Draft_013 is current FINAL.
- 2026-10-03 — Created Draft_014 from Draft_013: Appendix A layout —
  Quick-Reference and Legend side-by-side in 2-col table; Coding Sheet
  + Combined Example moved before Full Codebook; Full Codebook forced
  to new page; intro text updated; fonts tightened in quick block.
- 2026-10-03 — Draft_014 revised: left original QR alone; Legend + Coding Sheet + Combined Example on their own new page (fitted); Full Codebook on following new page.
- 2026-10-03 — Draft_014 fixed: Legend/Coding/Combined moved with original table colors, highlights, and styling preserved; only modest para spacing so the block fits one page.
- 2026-10-02 — Session `auto-1790954075-b54f1a` (Claude) opened: repo
  cloned via one-shot credential helper, remote clean, doctor passing.
  Reviewed Draft_013 (findings under Open Threads). PAT pasted in
  plaintext again (redacted); rotation recommended.
- 2026-10-02 — Created Draft_007 (from Draft_005): full narrative rewrite;
  title, RQs, Research Corpus section verbatim; redundancies cut. Fixed in
  passing: VM zero-hedge comparison (was "less than a third" for 40%/35%),
  booster average dropped (88/28 = 3.1, not 3.4), Scope no longer says boosters
  are not examined, timeline 24 weeks. Open: Landis & Koch (1977) cited but
  missing from References; Appendix A and C overlap.
- 2026-10-02 — Created Draft_006: full narrative rewrite (Intro–Recommendations)
  cutting redundancies; all verified citation claims retained; Refs +
  Appendix text included (color highlights remain in Draft_005 App D).
- 2026-10-02 — Overwrote Draft_005: accuracy fixes (Afshar n=180;
  majority→nearly half; Biology non-epistemic wording); prior
  Escalona/Khunasathitchai/APA/App E fixes retained.
- 2026-10-02 — Session `auto-1790912622-eb658c` (Claude) opened: repo
  cloned via one-shot credential helper, remote URL clean, hooks
  installed, doctor.sh passing. PAT pasted in plaintext again (redacted
  in transcript); rotation recommended.
- 2026-10-02 — Session `auto-1790903296-02e608` (Grok) opened.
  Repo cloned, token stripped from remote URL, hooks installed,
  transcript started. PAT redaction count incremented to seven.
- 2026-09-10 — Pushed `003_ThesisProposal_Draft_003.docx` (writing-
  voice pass per preferences.md: tighter, more direct prose in
  Background and Conclusions). Prior drafts retained.
- 2026-09-10 — Pushed `003_ThesisProposal_Draft_002.docx` (claim
  consistency + Table 6 / Recommendations softening). Draft_001 kept
  in working tree per user request.
- 2026-09-08 — Synced preferences.md from ai-mem2 repo. Four edits
  applied; ai-mem2 designated canonical source for preferences.md.
  See `decisions.md`.

## Blockers
_None._
