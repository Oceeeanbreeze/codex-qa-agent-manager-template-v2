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
- Prefer `getByTestId` and project-standard helpers over brittle DOM chains.
- Use explicit assertions.
- Do not fix a failed test until failure triage is complete.
- Document selector debt, auth blockers, and cleanup assumptions when relevant.
- Do not rely on Russian UI text, labels, or headings when a stable test id exists or can be requested.
- Do not add per-test login when project auth setup or suite-level reuse is already available.
- Account for Chromium, Firefox, and WebKit compatibility.
- Add `test.step` for meaningful phases of the scenario.
- Use `expect.soft` only for secondary checks, never for the core business outcome.
- Prefer created entity names with the `AT` prefix.
- Keep the test independent from other tests.

## Workflow

1. Read the good Playwright examples first.
   Path: `skill-design-inputs/playwright-good/`
2. Read the project practices reference.
   Path: `references/project-practices.md`
3. Read the review checklist reference before finalizing.
   Path: `references/review-checklist.md`
4. If a matching manual testcase exists, align the test to that goal.
   Paths:
   `skill-design-inputs/manual-testcase-regulation/REGULATION.md`
   `skill-design-inputs/manual-testcases-good/`
5. Reuse existing project helpers, fixtures, and conventions.
6. Prefer the smallest maintainable change set.
7. If the required behavior is still unclear, stop at assumptions instead of inventing hidden product logic.

## Review checklist

Before finalizing, verify:
- selector choice is justified and primarily based on `data-test-subj`;
- waits are not masking instability;
- assertions match the business outcome;
- test structure is easy to maintain;
- setup and cleanup are deterministic enough for CI;
- suite structure respects the project's auth and page-lifecycle strategy;
- the test remains safe under all configured browser projects.

## Project-specific rules

Apply these rules unless the repository clearly uses a different pattern:

- Prefer project auth setup and `storageState` over repeated UI login.
- If the suite uses a singleton page pattern, open the page in `beforeAll`, store it in a suite variable, and reuse it across tests in that suite.
- When singleton page mode is used, do not casually switch back to `{ page }` fixture style inside the same suite.
- Reuse existing helpers such as route openers, loader waits, auth checks, and fatal-app guards before writing local replacements.
- Prefer `data-test-subj` selectors through `getByTestId`.
- Avoid `getByText`, `getByLabel`, placeholder-based locators, and CSS-only locators when they depend on localization or unstable UI wording.
- If a fallback localized locator is temporarily unavoidable, mark it as selector debt in comments or handoff notes.
- Include `SMTEST` case id in the test or describe naming when the source testcase provides it.
- Preserve project tags and metadata conventions for priority, depth, and related markers.
- Use explicit skip reasons.
- Use explicit expect messages for non-obvious failures.
- Add short comments only around genuinely important implementation choices.

## Current source practices

The current project examples show:
- `test.describe.configure({ mode: 'serial' })` at suite level;
- suite-level `beforeAll` creating a shared `Page` via `browser.newPage()`;
- `storageState` auth configured in Playwright config through `auth.setup.ts`;
- widespread use of `getByTestId('data-test-subj-value')`;
- existing helper functions for route opening, login fallback, loader waits, and fatal error checks.

## If only partial artifacts exist

When only good examples are available:
- infer style from those examples;
- keep the implementation conservative;
- avoid introducing advanced patterns that are not present in the reference tests yet.
