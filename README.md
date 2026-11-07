# Revvel Hail

Governance and project home. All work follows [revvel-standards](https://github.com/midnghtsapphire/revvel-standards) OWNER RULES:

<!-- 2026-11-07, Cursor cloud agent (Grok 4.7), reason: superseded as an absolute ban. Ordinary work is still never deleted. This comment does not grant permission to rewrite history. The replacement states secret-remediation precedence. PR https://github.com/midnghtsapphire/revvel-hail/pull/3
- NEVER delete. Comment out with dated note instead.
-->
- Ordinary work is never deleted. Comment out superseded wording in place with a dated note (date, agent, reason, PR) and keep the original visible. If a credential is exposed, do not publish it and do not copy it into a comment, commit, log, screenshot, or artifact to preserve history. Do not auto-rewrite git history. Secret remediation follows the path the owner has approved. This file does not grant permission to rewrite history. Precedence: never-delete governs ordinary work. It does not authorize keeping a live secret in the repo, and it does not itself authorize an agent to erase history.
- NEVER rewrite wholesale. Additions only; original stays visible.
- Keeping an original visible does not mean copying a secret into the file or into a comment.
<!-- 2026-11-07, Cursor cloud agent (Grok 4.7), reason: superseded because everything was read as requiring unsanitized logs, private reasoning, and secrets in the repo. PR https://github.com/midnghtsapphire/revvel-hail/pull/3
- Everything goes in the repo. No vapor.
-->
- Ship task artifacts as you go. That covers code, docs, tests, sanitized command and outcome records, skill names, API, MCP, and CLI names and versions, sources, and concise decision summaries (conclusion, evidence, alternatives and tradeoffs). Do not require hidden chain-of-thought, private internal reasoning, hidden prompts, or private provider transcripts. No tokens, passwords, private keys, environment dumps, credentials, personal data, or protected content in commits, command arguments, logs, screenshots, or egress. Credentials stay in approved vault or secret stores. Record references only. Inspect and sanitize before push. Retain safe metadata rather than silently losing the work. No new destinations or widened access without user authorization.
<!-- 2026-11-07, Cursor cloud agent (Grok 4.7), reason: superseded because agents do not merge their own PRs did not name merge authority and could be read as a self-merge-only ban or as a blanket delegation. PR https://github.com/midnghtsapphire/revvel-hail/pull/3
- Draft PRs for owner review where possible. Agents do not merge their own PRs.
-->
- Agents prepare and integrate task branches and draft PRs for review. Merge authority remains the owner, or a delegate the owner has specifically authorized for that merge, where the authorization is verified to apply and the required review gates are satisfied. An agent's claim of approval is not authorization. Do not turn the old self-merge ban into a blanket delegation.
<!-- 2026-11-07, Cursor cloud agent (Grok 4.7), reason: superseded as an absolute that was read as forbidding owner-approved secret remediation and as requiring secrets to remain in history. Ordinary history stays append-only. This comment does not grant a history rewrite. PR https://github.com/midnghtsapphire/revvel-hail/pull/3
- Append-only history.
-->
- Ordinary history is append-only. A secret exposure does not create permission to publish the secret so the history stays intact, and it does not create permission for an agent to rewrite history. Follow owner-approved secret remediation. Never auto-rewrite history.

Projects live under `docs/<project-name>/`.

- Fleet orchestrator operating prompt: [`docs/orchestrator/`](docs/orchestrator/) (added 2026-11-06).

## Agent identity & permissions rule (added 2026-11-04, requested by Audrey)

Every agent, visiting agents included, must do this the first time it works in this repo, before any other change:

1. **Say who it is.** Exact platform: Claude Code (CLI) / Claude.ai (web or app chat) / Claude cloud worker (Claude Code on the web, background or cloud agent) / Cursor cloud agent / Grok Bot (give the bot's name, e.g. Proofy) / Grok web or main / ChatGPT or Codex / GitHub Copilot / other. Add the model if known.
2. **Say which GitHub identity it acts as.** That means the account, GitHub App, or token type. Many agents post as `midnghtsapphire`, so say so if that applies.
3. **List its GitHub permissions.** Cover read/write/admin, which repos, whether it can merge, run Actions, create repos, and post Discussions. For each one, say either **"Audrey can change this"** (and where: fine-grained PAT settings, classic token scopes, GitHub App installation settings, repo collaborator settings, branch protection) or **"fixed by the platform (it is what it is)"**. Mark anything it could not check as `[VERIFY]`. Never paste tokens.
4. **Add the date.**
5. **Write it down** in [`docs/ledgers/AGENT-REGISTRY-LEDGER.md`](docs/ledgers/AGENT-REGISTRY-LEDGER.md), append-only, using the template there. Update its row in [`AGENT-PERMISSIONS.md`](AGENT-PERMISSIONS.md), adding a row if it has none.
6. **Log each work session.** Every session appends a short "who did what" entry to that ledger, with commit SHAs or PR links.

The ledger is the history. AGENT-PERMISSIONS.md is the current state.

- Agent permissions lookup table: [AGENT-PERMISSIONS.md](AGENT-PERMISSIONS.md) (added 2026-11-04)
