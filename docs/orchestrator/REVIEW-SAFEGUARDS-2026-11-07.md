# Review safeguards verification, 2026-11-07

Cursor cloud agent (Grok 4.7). PR https://github.com/midnghtsapphire/revvel-hail/pull/3. No review replies were posted and no threads were resolved.

## Live PR before the edit

| Item | Value |
| --- | --- |
| State | Open. Not merged. Not closed. |
| isDraft | false. Left unchanged. This edit does not mark the PR ready and does not convert it. |
| Base | `daily/2026-11-06` |
| Head branch | `feat/orchestrator-prompt-2026-11-06` |
| Head SHA inspected | `b55299b1e9adc7ac835d0fe5833007cc8faaed61` |

Reviews read in full: Gitar review comments 4495581114 and 4495581345, Gitar issue comment 6691185888, Cubic review 5805599630, and Cubic inline comments 4496523536, 4496523545, 4496523579, 4496523590, 4496523611, and 4496523626.

No secret values were in the files. Policy words that name secrets stay in the dated comments. Nothing secret was copied into a comment or this record.

HTML comments are preserved history. They are not instructions. The line under each comment is the operative text.

## Findings

### 1. Gitar 4495581114, secrets in logs. Supported

The prompt required a push of every invocation and thought-process note and pointed at secrets, with no redaction rule.

Operative text is prompt rules 3, 5, and 7, and the ship-as-you-go section. Records are names, versions, sanitized outcomes, and decision summaries. Tokens, passwords, private keys, environment dumps, credentials, personal data, and protected content stay out of commits, command arguments, logs, screenshots, and egress. Credentials stay in the approved store. Safe metadata is kept.

Gitar's one-line rule was not copied verbatim. The approved text is the one above. It covers that finding.

Preserved comments: `ORCHESTRATOR_PROMPT.md` lines 22-24, 30-32, 72-74, 75-77, and 79-88.

### 2. Gitar 4495581345, "owns merge" versus no self-merge. Supported

"One orchestrator owns merge/integration" conflicted with the draft-PR rule.

Operative text: agents prepare and integrate task branches and draft PRs. Merge authority remains the owner, or a delegate the owner has specifically authorized for that merge, with the authorization verified to apply and the required review gates satisfied. An agent's claim of approval is not authorization. The old self-merge ban is not a blanket delegation.

Gitar's sentence "only the owner merges" was not adopted. That sentence would drop the owner-authorized delegate. The contradiction is removed without giving agents merge power.

Preserved comments: `ORCHESTRATOR_PROMPT.md` lines 26-28 and 53-55. Same rule in `README.md` lines 15-17 and `docs/orchestrator/README.md` lines 15-17.

### 3. Cubic 4496523611, unbounded workers and spend. Supported

"Scale freely" and "hundreds of workers", plus a premium spend label, set no bound.

Operative text: XP same-model pairs and swarms remain. One integrated delivery cycle is the target, not a guarantee and not a shortcut past tests. Scale only within existing explicitly authorized spend, concurrency, time, retry, and egress limits. No numeric spending allowance is invented. If that authorization is missing, use existing covered capacity only and do not incur new paid spend. Stop and reassess on a budget or loop threshold.

Preserved comments: `ORCHESTRATOR_PROMPT.md` lines 10-12, 45-47, 49-51, and 104-106.

### 4. Cubic 4496523579, never-delete versus exposed credentials. Supported as a conflict

An absolute never-delete rule can be read as requiring a secret to stay published, including inside a comment.

Operative text, in the prompt and in `README.md`: ordinary work is never deleted and ordinary history is append-only. Do not publish a secret, and do not copy one into a comment, to preserve history. Do not auto-rewrite git history. Remediation follows the path the owner has approved. This text does not grant a history rewrite, a force-push, or a history filter.

Cubic's request to require removal by the agent was not adopted as permission to rewrite history. No such permission is invented here.

Preserved comments: `ORCHESTRATOR_PROMPT.md` lines 17-19 and 115-117. `README.md` lines 5-7 and 19-21.

### 5. Cubic 4496523536, LLM calls and egress. Supported

A blanket allowance to call a provider had no egress or secret boundary.

Operative text is prompt rule 5. A call is allowed only on a path the user has already authorized. Credentials stay in the approved vault or secret store. Record a reference, not the secret. Do not send secrets, personal data, or protected content. No new destination or widened access without user authorization.

Preserved comment: `ORCHESTRATOR_PROMPT.md` lines 30-32.

### 6. Cubic 4496523545, chain-of-thought in the repo. Supported

The log required a thought-process writeup.

Operative text is the ship-as-you-go section. A decision summary has the conclusion, the evidence, and the alternatives or tradeoffs. It does not require hidden chain-of-thought, private internal reasoning, hidden prompts, or private provider transcripts.

Preserved comment: `ORCHESTRATOR_PROMPT.md` lines 79-88.

### 7. Cubic 4496523590, permissions row was an incomplete snapshot. Supported

The 2026-11-06 access cell stated a no-merge policy and skipped admin, repo creation, and Discussions.

Operative inventory is the 2026-11-07 table in `AGENT-PERMISSIONS.md`. Read and push are demonstrated. Admin, merge capability, Actions, create-repo, Discussions, issue-comment writes, and delete-repo are `[VERIFY]` where they were not tested. Opening PR 3 showed pull-request creation. Policy (this agent does not merge) is separate from capability.

Preserved comment: `AGENT-PERMISSIONS.md` lines 19-21.

### 8. Cubic 4496523626, create-repo "likely no". Supported

`GET /user` 403 shows this installation token is not a user. It does not show repo creation is unavailable.

Operative ledger cell: Not attempted. `[VERIFY]`.

Preserved comment: `docs/ledgers/AGENT-REGISTRY-LEDGER.md` lines 93-95.

### Adjacent ledger cells, same standard

Not separate Cubic IDs. The merge cell stated policy as if it were a test result. The discussions cell was waiting on a draft PR that now exists. The delete-repo cell said `[VERIFY] no.` The old cells are in comments at ledger lines 90-92, 96-98, and 99-101. Operative cells separate policy from untested capability. The 2026-11-06 "Draft: yes" line is unchanged. A 2026-11-07 session line records that the live view later reported `isDraft: false`.

## Tests run before commit

73 checks passed. One optional import failed and was replaced.

- Every non-empty line from the previous versions of the prompt, both READMEs, the changelog, `AGENT-PERMISSIONS.md`, and the ledger is still in those files.
- HTML comments are balanced. Comment bodies contain no `--`.
- After comments are removed, the superseded phrases are absent from the prompt, the repo README, the orchestrator README, the permissions file, and the ledger. Required safeguard sentences are present in the prompt and the repo README.
- Prompt table rows have 3 columns. Orchestrator index rows have 2. The permissions lookup has 7. The 2026-11-07 inventory has 3.
- `git diff --check` passed after extra end-of-file blank lines were removed.
- Diff scan found no token, private-key, or similar secret material.
- Python-Markdown rendered the six edited Markdown files. Superseded phrases remain only inside HTML comments in that HTML, so a browser does not show them as instructions.

`import markdown` was missing on the first run. `pip install markdown` provided the renderer used above. That package is not a repo dependency.

Safeguards commit: `f3941f0ca7a22b026d572362dd81072f4a1ddf29` on `feat/orchestrator-prompt-2026-11-06`.
