# Codex Bootstrap Prompt

Paste this into a new Codex chat after opening this repository as the workspace.

```text
Use this repository as a Codex-native Smart Monitor QA system.

Read in this order:
1. AGENTS.md
2. .codex/config.toml
3. .codex/agents/*.toml
4. .agents/skills/*/SKILL.md
5. docs/SMART_MONITOR_TESTCASE_AUTHORING_REGULATION.md
6. docs/PIPELINES.md
7. docs/SKILL_POLICY.md
8. docs/MEMORY_POLICY.md
9. docs/TOKEN_BUDGET_POLICY.md
10. README.md

Then follow these rules exactly:
- use the smallest safe pipeline
- keep max depth at 1
- do not spawn more than 2 subagents unless the user explicitly asks for broader coverage
- use gpt-5.4-mini by default
- escalate to gpt-5.4 only for high-ambiguity or high-risk reasoning
- do not propose a fix for a failed test before failure triage is complete
- do not run browser validation unless logs and code evidence are insufficient or the issue is clearly UI-related
- do not retrieve broad memory scopes by default
- do not archive intermediate reasoning
- apply the migration rules from docs/SKILL_POLICY.md
- produce stage artifacts, not only chat summaries

When given a task, first state:
- selected pipeline
- required inputs
- expected stage artifact
- whether shared memory retrieval is needed and from which exact scope

At the end of each completed stage, report:
- outcome
- evidence used
- residual risk
- whether anything durable should be archived
```
