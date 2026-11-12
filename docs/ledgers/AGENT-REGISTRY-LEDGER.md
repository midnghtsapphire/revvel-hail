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

### 2026-11-06: Cursor cloud agent, ARRIVAL
- Platform: Cursor cloud agent (cloud/background agent).
- Model (if known): grok-4.7-high-fast (Grok 4.7).
- Acts on GitHub as: Cursor GitHub App. `gh auth status` reports account `cursor` with a `ghs_` installation token. Commit author is `Cursor Agent <cursoragent@cursor.com>`. Does not post as Audrey's user `midnghtsapphire`.
- How verified: `gh auth status`; `gh api user` (403, "Resource not accessible by integration"); `gh api repos/midnghtsapphire/revvel-hail` (default branch `main`; permissions object all false); branch-protection GET on `main` (403). No token pasted. Run: https://cursor.com/agents/bc-90ec15d8-825e-5907-bc23-7e8783c0e502. Owning user on the run: Audrey Evans.
- Permissions:
  | Capability | Has it? | Audrey can change it? (where/how) or fixed by platform |
  |---|---|---|
  | Read repos (which) | Yes for this checkout of `midnghtsapphire/revvel-hail`, and contents read of `midnghtsapphire/revvel-standards` succeeded. | Yes for which repos: GitHub App installation settings for Cursor. The permission set is fixed by the platform. |
  | Write/push (which repos) | Expected on the task branch of revvel-hail via the cloud-agent git remote. Permissions JSON returned all false [VERIFY against the push of this branch]. | Same as above. |
  | Admin | Not shown. Permissions JSON admin=false. `/user` is 403. | Fixed for this app token unless Audrey uses a different credential. |
  | Merge PRs | Not used. This agent does not merge its own PRs. Whether the app can merge is [VERIFY]; branch protection could not be read (403). | Yes: branch protection or rulesets. App install can be removed. |
  | Run/edit Actions workflows | Not tested. Existing docs row says the Cursor app can monitor and re-run Actions [VERIFY this token]. | App permission list is fixed by the platform. |
  | Create repos | Not attempted [VERIFY]. | App installation settings. |
  | Post Discussions/issues/comments | PR creation is the intended write. Discussions on revvel-hail were off as of 2026-11-04 [VERIFY today]. | Repo feature settings; app install. |
  | Delete repos | Not attempted. No `delete_repo` check available on this integration token [VERIFY]. | Keep repo deletion off the app if GitHub exposes that setting. |
- Unverified: [VERIFY] push rights until this branch pushes. [VERIFY] branch protection on `main`. [VERIFY] whether the app can merge, create repos, or edit workflows.

### 2026-11-06: Cursor cloud agent, SESSION
- Did: added a thin pointer at `docs/orchestrator/XP-SWARM-ORCHESTRATOR.md` (orchestrator SSOT stays in revvel-standards; prompt not copied). Added one README line under "Agent orchestration". Appended this arrival. revvel-hail has no `daily/YYYY-MM-DD` branch, so the PR targets `main` and is not a draft. Not merged.
- Commits/PRs: this commit on `cursor/xp-swarm-orchestrator-pointer-e502`. PR URL recorded in the follow-up line after the PR exists.

### 2026-11-06: Cursor cloud agent, SESSION (follow-up)
- Did: push of `cursor/xp-swarm-orchestrator-pointer-e502` succeeded, so write/push on this repo is confirmed for this app token. Opened a normal PR into `main` (no `daily/` branch). Did not merge.
- Commits/PRs: `5bfe3122b63fa65105f195662cdf22bbeaa9fe72`; https://github.com/midnghtsapphire/revvel-hail/pull/4

### 2026-11-12: Manus (Manus AI agent), ARRIVAL
- Platform: other: Manus (Manus AI agent), running in a Manus cloud sandbox and driven from the Manus desktop app on Windows.
- Model (if known): not recorded by the platform in this session [VERIFY].
- Acts on GitHub as: **`midnghtsapphire`**, through a GitHub App user-to-server token (prefix `ghu_`) from the Manus GitHub connector. The token is stored in the sandbox `gh` CLI (`~/.config/gh/hosts.yml`). Posts as midnghtsapphire: **yes**. Commits carry `Co-authored-by: Manus <dev-agent@manus.ai>`.
- How verified (2026-11-12, about 13:15–15:26 MT): `gh auth status`, `gh api user`, `gh api repos/midnghtsapphire/<repo> --jq .permissions` for revvel-hail, revvel-standards, manus and deck-to-video-kit, plus the outcomes of the actual calls listed below. No tokens were pasted.
- Permissions:
  | Capability | Has it? | Audrey can change it? (where/how) or fixed by platform |
  |---|---|---|
  | Read repos (which) | Yes: every repo `midnghtsapphire` can reach (checked on 4) | Yes. Manus connector settings, or GitHub → Settings → Applications → Manus app access |
  | Write/push (which repos) | Yes: pushed to `deck-to-video-kit`, plus branches on `manus`, `revvel-standards` and `revvel-hail` | Same as above |
  | Admin | API reports `admin: true` on all 4 repos. However, `POST /repos/{repo}/pages` returned **403 Resource not accessible by integration**, and so did `GET /check-suites/{id}`, so the app does not get every admin endpoint | The app's permissions are fixed by the Manus GitHub App. Audrey can enable Pages herself in repo Settings |
  | Merge PRs | Technically possible (no branch protection was checked). **Policy: never merges its own PRs** (AGENTS.md rule 6) | Yes, add branch protection |
  | Run/edit Actions workflows | Edit: yes (pushed 4 workflow files). Run: every run ends in `startup_failure`, which is account-level billing, not the app | Yes, GitHub → Settings → Billing → Actions |
  | Create repos | Yes: created private `midnghtsapphire/deck-to-video-kit` | Yes, through the connector settings |
  | Post Discussions/issues/comments | Turned on Discussions for `deck-to-video-kit`; opened draft PRs | Yes, through the connector settings |
  | Delete repos | Not tested and will not be tested (AGENTS.md rule 2) [VERIFY] | Yes, through the connector settings |
- Unverified: [VERIFY] model name; [VERIFY] whether repo deletion is allowed.

### 2026-11-12: Manus (Manus AI agent), SESSION
- Did: built and shipped the Deck-to-Video Kit from Audrey's 30-second Taplio deck video. Created the private repo `midnghtsapphire/deck-to-video-kit` and Release `v1.0.0` (Playbook PDF $19, Full Kit $49, done-for-you from $299). Put the public store page on Manus hosting at https://deck2vid-fenbmfwl.manus.space/; Audrey approved public visibility. Opened tracking draft PRs in `manus`, `revvel-standards` and this repo. Merged nothing.
- Commits/PRs: `deck-to-video-kit` `65cc781` (initial), plus https://github.com/midnghtsapphire/deck-to-video-kit/pull/2 (draft). The draft PRs in `manus`, `revvel-standards` and `revvel-hail` are listed in `deck-to-video-kit/docs/governance/TRACKING.md`.
