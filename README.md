# thesis-memory

Persistent memory for chat with AI agents. A private GitHub repo holds a few
markdown files and verbatim session transcripts. The agent reads them at the
start of a session and updates them as you work.

## Files

| File / Dir | Purpose |
|---|---|
| `context.md` | Session start protocol and current focus. Read first. |
| `preferences.md` | How you want the assistant to write and behave. |
| `knowledge.md` | Facts you share. |
| `projects.md` | Active and past projects. |
| `decisions.md` | Durable decisions, append-only. |
| `lessons.md` | Mistakes and fixes. Never archived. |
| `chat_history/` | Verbatim transcripts, per model per session. |
| `thesis/` | Thesis drafts and working files. |
| `RETRIEVAL.md` | Agent guide for the search tools. |
| `TRANSCRIPT_REMINDER.md` | Failsafe reminder to log each message. |
| `scripts/` | Secret scanners, hook installer, session and retrieval tools. |
| `.github/workflows/` | Secret scan, transcript check, size check. |

## Setup

1. **Create a fine-grained token** at github.com/settings/tokens. Limit it
   to this repo, grant Contents read and write (plus Workflows if CI
   changes need to push), and set a short expiry. Copy it once.

2. **Install the hook.** `.git/hooks/` isn't version controlled, so every
   fresh clone needs this. It scans commits for secrets and blocks memory-file
   changes that come without a transcript update:

   ```sh
   ./scripts/install_hooks.sh
   ```

3. **Paste this at the start of each chat:**

   ```
   Use my private GitHub repo as persistent memory.

   Repo: https://github.com/ckmanuel/thesis-memory.git
   Token: <token, or $GH_PAT if your environment keeps env vars>

   At session start: clone the repo, remove the token from the remote URL,
   then follow the "FIRST ACTION AT SESSION START" block in context.md.

   During the session: follow context.md for transcript logging. Update
   existing memory entries instead of duplicating them. Commit and push
   after meaningful work using a one-shot credential helper that reads the
   token from the environment. Never write the token into any file or into
   .git/config. The "never commit the token" rule overrides "verbatim
   transcript": redact it.
   ```

## Retrieval tools

Once `chat_history/` grows, use the tools in `scripts/` to find things in
past sessions. `RETRIEVAL.md` explains when and how, and the agent reads it
at session start. For semantic search, run `pip install -r
scripts/requirements.txt` once. The embeddings DB lives at
`~/.cache/ai-memory-embeddings.db`, outside the repo, and can be deleted and
rebuilt. The first build downloads a model of about 80MB.

## Token handling

The scanners block commits containing token shapes, and CI scans again on
push. That protects the repo, not the chat. Web agents run in throwaway
workspaces, so you usually have to paste the token into the chat, where it
stays in the log. Treat it as exposed once pasted. Scope it to one repo, keep
the expiry short, and revoke it when the session ends. If a token ever lands
in a commit, rotate it immediately.

## Binaries

`.gitignore` blocks PDFs, images, office files, and media. Every pushed
binary stays in git history forever. Keep deliverables outside the repo, or
force-add one deliberately with `git add -f`.

## Credits

The pattern (private repo, opening prompt, per-session transcripts) comes
from the [Persistent Memory Guide](https://persistent-memory-deploy.vercel.app/)
by [Rommark.Dev](https://rommark.dev), built with Z.ai. The scanners, CI
workflows, retrieval tools, and session scripts were added in collaboration
with the GLM assistant on chat.z.ai.
