# Smart Monitor Agent System V2

This repository is a clean-start Codex-native subagent system for Smart Monitor QA automation.

It is designed for four concrete outcomes:
- regulated manual testcase generation;
- Playwright automation generation and maintenance;
- failure analysis for broken autotests;
- safe repair proposals and test fixes after triage.

This repository intentionally optimizes for:
- clear stage ownership;
- low token waste;
- shared team memory with local rebuildable indexes;
- deterministic artifact outputs instead of long free-form chat.

## Core design rules

- Use native Codex subagents from `.codex/agents/*.toml`.
- Keep routing cheap and specialist work narrow.
- Analyze failures before proposing fixes.
- Store only approved knowledge in shared memory.
- Treat markdown as source of truth and indexes as rebuildable caches.
- Prefer `gpt-5.4-mini` by default and use `gpt-5.4` only for high-ambiguity or high-risk reasoning.

## Minimal repository structure

```text
smart-monitor-agent-system-v2/
  README.md
  AGENTS.md
  .gitignore
  .agents/
    skills/
      smart-monitor-scenario-pack-writer/
        SKILL.md
      smart-monitor-playwright-automation-writer/
        SKILL.md
      smart-monitor-playwright-review-checklist/
        SKILL.md
      smart-monitor-failure-triage/
        SKILL.md
      smart-monitor-browser-evidence/
        SKILL.md
      smart-monitor-test-repair-policy/
        SKILL.md
      smart-monitor-token-budget-guard/
        SKILL.md
  .codex/
    config.toml
    agents/
      router.toml
      researcher.toml
      scenario-designer.toml
      test-automation-engineer.toml
      failure-triager.toml
      qa-browser.toml
      reviewer.toml
      archivist.toml
  docs/
    CODEX_BOOTSTRAP_PROMPT.md
    PIPELINES.md
    MEMORY_POLICY.md
    TOKEN_BUDGET_POLICY.md
```

## Start here

1. Read `AGENTS.md`.
2. Read `docs/PIPELINES.md`.
3. Read `docs/SMART_MONITOR_TESTCASE_AUTHORING_REGULATION.md`.
4. Read `docs/SKILL_POLICY.md`.
5. Review `.agents/skills/` to see the current repo-scoped skill set.
6. Read `docs/MCP_STRATEGY.md`.
7. Read `docs/MCP_MATRIX.md`.
8. Read `docs/MCP_SETUP.md`.
9. Read `docs/MEMORY_POLICY.md`.
10. Read `docs/TOKEN_BUDGET_POLICY.md`.
11. Paste `docs/CODEX_BOOTSTRAP_PROMPT.md` into a new Codex chat for this repo.

## Shared memory model

Use one shared markdown vault for approved QA knowledge and one local index store per operator.

- Shared source of truth:
  - testcase standards
  - scenario packs
  - automation specs
  - failure dossiers
  - repair reports
  - known issues
- Local rebuildable caches:
  - vector indexes
  - lexical indexes
  - sqlite stores

Do not share secrets, cookies, tokens, HAR files, raw traces, or raw screenshots.

## Success criteria

The system is successful only if it can:
- produce a regulated testcase from a request without overloading context;
- generate or update a focused Playwright test from an approved scenario;
- classify a failed test into a clear failure category before proposing a fix;
- explain whether the problem is in the product, the test, the selector, auth, data, or the environment;
- preserve approved team knowledge without turning memory into noisy chat history.
