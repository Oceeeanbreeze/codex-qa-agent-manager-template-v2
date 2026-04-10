# Developer Triage Workflow

## Goal

Provide a narrow Smart Monitor workflow for a frontend developer who needs to:
- analyze failed Playwright tests;
- distinguish product bugs from test failures;
- produce a concise diagnosis report;
- repair the test only after triage confirms the problem is test-side.

This workflow is not the full QA system.
It is a developer-focused mode of V2.

## Use this mode when

- a Playwright test failed and the developer needs a focused diagnosis;
- the likely causes include selector drift, auth issues, stand issues, flaky timing, or test code defects;
- the developer should not run the full testcase-generation and broader QA-planning pipeline.

## Agent set for developer mode

### Required
- `router`
- `researcher`
- `failure-triager`
- `reviewer`

### Conditional
- `test-automation-engineer`
- `qa-browser`

### Disabled by default in developer mode
- `scenario-designer`
- broad archival flows
- coverage planning flows
- broad shared-memory retrieval

## Default pipeline

### Failure diagnosis only
- `router -> researcher -> failure-triager -> reviewer`

Output:
- `failure-dossier`

### Failure diagnosis plus test repair
- `router -> researcher -> failure-triager -> test-automation-engineer -> reviewer`

Output:
- `failure-dossier`
- code patch
- `repair-report`

### Failure diagnosis plus browser evidence
- `router -> researcher -> failure-triager -> qa-browser -> reviewer`

Output:
- `failure-dossier` with browser evidence

## Hard rules

- Never repair a failed test before `failure-triager` completes.
- Never run `qa-browser` by default.
- Never treat a product bug as a test-fix request.
- Never run broad memory retrieval across all team folders.
- Never archive transient debugging notes as durable shared memory.

## Failure categories

Every diagnosis must classify the failure into:
- `selector-drift`
- `auth-or-stand`
- `timing-or-flake`
- `test-data`
- `test-bug`
- `product-bug`
- `unknown`

The diagnosis must include:
- confidence
- evidence used
- what still remains uncertain
- whether a browser check is required

## When test repair is allowed

The system may propose or implement a test fix only when:
- the failure is classified as `selector-drift`, `timing-or-flake`, `test-data`, or `test-bug`
- the triage contains enough evidence to justify the fix
- the reviewer can validate that the fix matches the diagnosed cause

The system must not auto-repair when:
- the likely cause is `product-bug`
- the likely cause is `auth-or-stand` but the environment is still unstable
- the classification is `unknown`

## Memory scope for developer mode

Prefer these scopes only:
- `SmartMonitor/Failures/`
- `SmartMonitor/Repairs/`
- `Standards/Playwright/`
- `Known-Issues/`

Avoid these by default:
- full testcase libraries
- broad exploratory QA notes
- broad strategy and coverage notes

## Token policy for developer mode

- default model: `gpt-5.4-mini`
- escalate only on ambiguous or high-risk triage
- maximum active subagents by default: `2`
- browser runs only by trigger
- summarize logs before reasoning on them

## Definition of done

Developer mode is successful only when it returns:
- a clear failure category
- a concise diagnosis
- a statement of whether this is product-side or test-side
- a safe repair proposal only if triage allows it
