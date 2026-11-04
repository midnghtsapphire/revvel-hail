# Agent Registry Ledger (append-only)

Started 2026-11-04 at Audrey's request. This is the history of who each agent is, what GitHub access it has, and what it did. Rules are in the [README](../../README.md#agent-identity--permissions-rule-added-2026-11-04-requested-by-audrey). The current state is in [AGENT-PERMISSIONS.md](../../AGENT-PERMISSIONS.md).

**Append only.** Never edit or delete earlier entries. If something was wrong, add a dated correction below it.

## Template (copy, paste, fill in)

```markdown
### YYYY-MM-DD: <agent name>, ARRIVAL
- Platform: Claude Code (CLI) | Claude.ai (web/app) | Claude cloud worker | Cursor cloud agent | Grok Bot "<name>" | Grok web/main | ChatGPT/Codex | Copilot | other: ___
- Model (if known): ___
- Acts on GitHub as: <account / GitHub App / token type> (posts as midnghtsapphire? yes/no)
- How verified: <commands run or docs read; no tokens pasted>
- Permissions:
  | Capability | Has it? | Audrey can change it? (where/how) or fixed by platform |
  |---|---|---|
  | Read repos (which) | | |
  | Write/push (which repos) | | |
  | Admin | | |
  | Merge PRs | | |
  | Run/edit Actions workflows | | |
  | Create repos | | |
  | Post Discussions/issues/comments | | |
  | Delete repos | | |
- Unverified: [VERIFY] ___

### YYYY-MM-DD: <agent name>, SESSION
- Did: ___
- Commits/PRs: ___
```

---

### 2026-11-04: Proofy, ARRIVAL
- Platform: Grok Bot "Proofy", Audrey's book-proofing assistant, working through a shell on its own box with the `gh` CLI. This entry was written by Proofy's executor subagent.
- Model: not stated here. Platform identity is Grok Bot.
- Acts on GitHub as: **`midnghtsapphire`** (Audrey's own user account) through a `gh` CLI login stored on the Grok Bot box. Commits and comments look like Audrey's.
- How verified (2026-11-04, ~09:20 MT): `gh auth status`, `gh api user`, `gh api repos/midnghtsapphire/revvel-hail --jq .permissions`, the `X-OAuth-Scopes` response header, `gh api repos/midnghtsapphire/revvel-hail/collaborators`, and `.../branches/main/protection`. No token was printed.
- Verified facts:
  - Token type: a classic OAuth token, since GitHub returned `X-OAuth-Scopes`. Its scopes are `gist`, `read:org`, `repo`, `workflow`.
  - revvel-hail permissions: admin, maintain, push, triage, and pull are all **true**. The repo is public, and the only collaborator is `midnghtsapphire` (admin).
  - Branch protection on `main` in revvel-hail: **none**. `main` is not protected, so this token can push straight to it.
  - `gh api /user/installations` returned 403, because that call only works with GitHub App user tokens. Installed GitHub Apps could not be listed this way.
- Permissions:
  | Capability | Has it? | Audrey can change it? |
  |---|---|---|
  | Read all repos Audrey can read | Yes (`repo` scope) | Yes. Revoke the token or sign `gh` out on the box. Or replace it with a fine-grained PAT limited to chosen repos: GitHub, Settings, Developer settings, Personal access tokens. |
  | Write/push to every repo Audrey owns | Yes (`repo`) | Yes. Same as above. A fine-grained PAT can be limited to read-only or to certain repos. |
  | Admin on revvel-hail | Yes (it acts as the owner) | Yes. Only by using a different, narrower token. Owner actions follow the account. |
  | Merge PRs | Yes, technically. The README rule says agents do not merge their own PRs. | Yes. Turn on branch protection or rulesets requiring review in repo Settings, then Branches. |
  | Edit Actions workflow files | Yes (`workflow` scope) | Yes. Remove the scope or use a fine-grained PAT without Workflows. |
  | Create repos | Yes (`repo` scope allows it) [VERIFY by test; not attempted] | Yes. Use a fine-grained PAT; it can't create user repos unless given Administration write [VERIFY]. |
  | Delete repos | No (`delete_repo` scope not present) | Yes. Keep that scope off. |
  | Discussions/issues/comments | Yes on repos where they're enabled. revvel-hail has Discussions **off**. | Yes. Repo Settings, then Features. |
  | Gists | Yes (`gist`) | Yes. Use a token without that scope. |
- What's fixed by the platform: Grok Bot can only use GitHub through whatever credential is on the box or connected as a connector. It has no separate bot identity unless Audrey gives it one, such as a machine-user account or a GitHub App.
- Unverified: [VERIFY] whether the Grok Bot GitHub connector (`GitHub-xai`) uses a different credential or app. [VERIFY] which GitHub Apps are installed on Audrey's account (check https://github.com/settings/installations).

### 2026-11-04: Proofy, SESSION
- Did: added the agent identity and permissions rule to README.md, created this ledger and AGENT-PERMISSIONS.md, and appended a pointer line in revvel-standards VISITING_AGENTS.md.
- Commits: see the follow-up line below.
