---
name: smart-monitor-playwright-automation-writer
description: Use when the task is to write or update Smart Monitor Playwright tests from approved scenarios or from already-triaged failures. Best for producing focused, maintainable Playwright tests that follow the team's preferred style.
---

# Smart Monitor Playwright Automation Writer

Write focused Playwright tests for Smart Monitor.

## Use this skill when

- a new Playwright autotest must be created from a known scenario;
- an existing Playwright test must be updated after confirmed triage;
- the user wants code that matches the team's preferred Playwright style.

## Hard rules

- One observable scenario equals one main test.
- Reuse existing helpers and fixtures before creating new ones.
- Prefer stable selectors over brittle DOM chains.
- Use explicit assertions.
- Do not fix a failed test until failure triage is complete.
- Document selector debt, auth blockers, and cleanup assumptions when relevant.

## Workflow

1. Read the good Playwright examples first.
   Path: `skill-design-inputs/playwright-good/`
2. If a matching manual testcase exists, align the test to that goal.
   Paths:
   `skill-design-inputs/manual-testcase-regulation/REGULATION.md`
   `skill-design-inputs/manual-testcases-good/`
3. Reuse existing project helpers, fixtures, and conventions.
4. Prefer the smallest maintainable change set.
5. If the required behavior is still unclear, stop at assumptions instead of inventing hidden product logic.

## Review checklist

Before finalizing, verify:
- selector choice is justified;
- waits are not masking instability;
- assertions match the business outcome;
- test structure is easy to maintain;
- setup and cleanup are deterministic enough for CI.

## If only partial artifacts exist

When only good examples are available:
- infer style from those examples;
- keep the implementation conservative;
- avoid introducing advanced patterns that are not present in the reference tests yet.
