---
name: smart-monitor-test-repair-policy
description: Use when a Smart Monitor Playwright test may be repaired after failure triage has already classified the problem as test-side. Best for safe, minimal fixes that match the diagnosed cause instead of masking real product or environment issues.
---

# Smart Monitor Test Repair Policy

Repair Smart Monitor Playwright tests only after confirmed triage.

## Use this skill when

- `failure-triager` has completed;
- the likely category is `selector-drift`, `timing-or-flake`, `test-data`, or `test-bug`;
- there is enough evidence to justify a narrow code change.

## Never repair when

- the likely category is `product-bug`;
- the likely category is `auth-or-stand` and the environment is still unstable;
- the result is still `unknown`;
- the only available change would hide the failure instead of explaining it.

## Main goal

Make the smallest repair that matches the diagnosed cause.

## Required output

Return or apply:
- a minimal patch plan;
- the exact diagnosed cause;
- the reason this fix is safe;
- residual risks;
- a short repair report.

## Hard rules

- Repair only what triage justified.
- Do not widen scope without new evidence.
- Do not replace a strong assertion with a weaker one just to make the test pass.
- Do not add sleeps to hide instability.
- Do not normalize weak localized selectors as permanent fixes.
- Prefer helper reuse, shared utilities, and project-standard patterns.

## Repair heuristics by category

### `selector-drift`

Allowed:
- switch from weak locator to stable `getByTestId`;
- update selector path to a known stable control;
- document selector debt if no stable test id exists yet.

Not allowed:
- replacing a broken selector with another equally weak localized selector without calling it out.

### `timing-or-flake`

Allowed:
- wait on stable visible state;
- wait on a known loader or ready signal;
- align checks to deterministic UI readiness.

Not allowed:
- arbitrary `waitForTimeout`;
- hiding race conditions without identifying the expected ready condition.

### `test-data`

Allowed:
- make test data unique or deterministic;
- align created entity naming with the `AT` prefix rule;
- isolate the test from stale shared data.

Not allowed:
- relying on uncontrolled existing state if the scenario can be made deterministic.

### `test-bug`

Allowed:
- fix wrong route, wrong helper usage, wrong assertion target, or wrong interaction sequence;
- align code to current project helpers and auth/session strategy.

Not allowed:
- broad refactors unrelated to the diagnosed bug.

## Smart Monitor-specific rules

- Respect project auth setup and `storageState`.
- Respect suite-level singleton page patterns where the suite already uses them intentionally.
- Keep browser-project compatibility in mind for Chromium, Firefox, and WebKit.
- Add `test.step` when repair work clarifies the scenario structure.
- Use `expect.soft` only for secondary checks, not for the business-critical outcome.
- Preserve `AT`, `SMTEST`, and project metadata conventions when they already exist or are required by the testcase.

## Final check before accepting the repair

Confirm all of these:
- the fix matches the triaged category;
- no product bug is being masked;
- no weak selector was silently normalized;
- the test remains maintainable;
- the review checklist would accept the change.
