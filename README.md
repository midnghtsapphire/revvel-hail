# Revvel Hail

Governance and project home. All work follows [revvel-standards](https://github.com/midnghtsapphire/revvel-standards) OWNER RULES:

- NEVER delete. Comment out with dated note instead.
- NEVER rewrite wholesale. Additions only; original stays visible.
- Everything goes in the repo. No vapor.
- Draft PRs for owner review where possible. Agents do not merge their own PRs.
- Append-only history.

Projects live under `docs/<project-name>/`.

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

## Agent orchestration

XP Swarm Orchestrator pointer (source of truth is revvel-standards): [docs/orchestrator/XP-SWARM-ORCHESTRATOR.md](docs/orchestrator/XP-SWARM-ORCHESTRATOR.md)
