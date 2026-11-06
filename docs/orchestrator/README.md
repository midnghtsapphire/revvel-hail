# Fleet orchestrator

Canonical operating prompt for fleet orchestrators. Added 2026-11-06 by PromptOrchestrator / Cursor cloud agent for Audrey Evans.

| File | What it is |
| --- | --- |
| [ORCHESTRATOR_PROMPT.md](ORCHESTRATOR_PROMPT.md) | The system prompt. This is the copy fleets load. |
| [CHANGELOG.md](CHANGELOG.md) | Dated additions. Append only. |

## How fleets use it

1. Read [ORCHESTRATOR_PROMPT.md](ORCHESTRATOR_PROMPT.md) at the start of an orchestration job and follow it as the operating prompt.
2. Keep owner rules from [revvel-standards](https://github.com/midnghtsapphire/revvel-standards) and this repo's [README](../../README.md). The prompt does not replace those.
3. Draft pull requests into `daily/YYYY-MM-DD`. Do not push straight to `main`. Do not merge your own PRs.
4. When the prompt changes, append a dated entry to [CHANGELOG.md](CHANGELOG.md). Leave the previous prompt text visible. Do not delete it.
