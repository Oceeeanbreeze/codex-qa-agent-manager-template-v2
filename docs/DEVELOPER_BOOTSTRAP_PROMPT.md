# Developer Bootstrap Prompt

Paste this into a new Codex chat after opening this repository as the workspace when the user is a frontend developer working on failed Playwright tests.

```text
Use this repository in Smart Monitor developer triage mode.

Read in this order:
1. AGENTS.md
2. .codex/config.toml
3. .codex/agents/*.toml
4. docs/DEVELOPER_TRIAGE_WORKFLOW.md
5. docs/MEMORY_POLICY.md
6. docs/TOKEN_BUDGET_POLICY.md
7. docs/SKILL_POLICY.md

Follow these rules exactly:
- optimize for failure diagnosis first, not for broad QA planning
- do not run testcase-generation flows
- do not propose a test fix until failure triage is complete
- use gpt-5.4-mini by default
- do not spawn more than 2 subagents unless explicitly justified
- do not run browser validation unless logs and code evidence are insufficient or the issue is clearly UI-related
- restrict memory retrieval to the smallest relevant scope, preferably failures, repairs, Playwright standards, and known issues
- do not archive transient debugging notes

When handling a failed test, first report:
- selected pipeline
- likely failure category candidates
- evidence available
- whether browser evidence is required

At the end, return:
- final failure category
- explanation of whether the problem is in the product or in the test
- confidence
- repair proposal only if allowed by triage
- residual uncertainty
```
