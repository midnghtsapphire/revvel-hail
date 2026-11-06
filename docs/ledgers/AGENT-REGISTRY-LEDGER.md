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
- Commits: revvel-hail e892aac3ee767a944e3be75b20b95792d67b7011; revvel-standards VISITING_AGENTS.md pointer (see that repo's history, 2026-11-04).

### 2026-11-06: Cursor cloud agent (Grok 4.7), ARRIVAL
- Platform: Cursor cloud agent
- Model (if known): Grok 4.7 (`grok-4.7-high-fast`)
- Acts on GitHub as: **Cursor GitHub App** (`gh` login `cursor`, GitHub App installation token). Posts as `midnghtsapphire`? **no**. Commit author on this box: `Cursor Agent <cursoragent@cursor.com>`.
- Run: https://cursor.com/agents/bc-b3dbdc9a-ad57-5cf6-b113-90e29d4cd8f8 (owned by Audrey Evans; email not copied into this public ledger)
- How verified: `gh auth status`, `gh api user` (403, app token is not a user), `gh api /installation/repositories`, `gh api repos/midnghtsapphire/revvel-hail` response headers and body, `gh api repos/midnghtsapphire/revvel-hail/rulesets`, contents read of `README.md`, and a push of `daily/2026-11-06` (same commit as `main`, no file changes). No token was printed.
- Verified facts:
  - This installation lists exactly one repo: `midnghtsapphire/revvel-hail`.
  - Contents read on that repo succeeded.
  - Push of a new branch succeeded (write is real).
  - `GET /repos/midnghtsapphire/revvel-hail/branches/main/protection` returned 403.
  - Rulesets list returned `[]`.
  - The repo JSON `permissions` object was all false. That conflicts with the successful contents read and branch push, so treat that object as unreliable for this app token. [VERIFY] why GitHub returns it that way.
  - revvel-hail is public. Discussions are off. Issues are on.
- Permissions:
  | Capability | Has it? | Audrey can change it? (where/how) or fixed by platform |
  |---|---|---|
  | Read repos (which) | Yes: `midnghtsapphire/revvel-hail` only, on this installation. | **Audrey can change which repos** in GitHub App installation settings (https://github.com/settings/installations, Cursor). **The app permission set is fixed by the platform.** |
  | Write/push (which repos) | Yes: pushed `daily/2026-11-06` to `midnghtsapphire/revvel-hail`. | Same as above. |
  | Admin | No evidence of admin. Branch protection read returned 403. | Same. Administration is not shown as granted. |
  | Merge PRs | Not attempted. This agent will not merge its own PRs. Rulesets on the repo are empty. [VERIFY] whether the token could merge if asked. | Audrey can add branch protection or rulesets under the repo Settings. The agent rule forbids merging anyway. |
  | Run/edit Actions workflows | Not attempted. [VERIFY] | App installation settings. Workflow runs may still need a human. |
  | Create repos | Not attempted. `GET /user` is 403. [VERIFY] likely no. | Creating repos is not something this installation token demonstrated. |
  | Post Discussions/issues/comments | Discussions are off on this repo. Issues are on. PR creation is the test for comments. [VERIFY until the draft PR exists] | Repo Settings, Features, plus the app's Issues/PRs permission (fixed by the platform). |
  | Delete repos | Not attempted. [VERIFY] no. | Keep that off. |
- Unverified: [VERIFY] full GitHub App permission list for the Cursor installation (contents, pull requests, issues, actions, administration). [VERIFY] whether branch protection exists on `main` (the protection endpoint was 403, and rulesets were empty).
