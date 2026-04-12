---
name: smart-monitor-failure-triage
description: Use when a Smart Monitor Playwright test has failed and the task is to classify the cause before any repair is proposed. Best for separating product bugs, test bugs, selector drift, auth or stand issues, and flaky timing from limited but real evidence.
---

# Smart Monitor Failure Triage

Diagnose failed Smart Monitor tests before any repair.

## Use this skill when

- a Playwright test failed;
- logs, traces, or code must be interpreted;
- the system must decide whether the failure is product-side or test-side;
- the next step depends on correct classification.

## Allowed categories

Every diagnosis must end in exactly one primary category:
- `selector-drift`
- `auth-or-stand`
- `timing-or-flake`
- `test-data`
- `test-bug`
- `product-bug`
- `unknown`

## Required output

Return a compact failure dossier with:
- failure category;
- product-side or test-side decision;
- confidence;
- evidence used;
- open uncertainty;
- whether browser evidence is required next;
- whether repair is allowed next.

## Hard rules

- Never propose code repair before classification is complete.
- Prefer `unknown` over overconfident guessing.
- Distinguish missing evidence from weak reasoning.
- If auth or environment instability is plausible, do not treat the issue as a clean test fix yet.
- If the logs do not support a product-bug claim, say so explicitly.

## Workflow

1. Read the failure artifact if one exists.
   Path: `skill-design-inputs/failures/`
2. Read the relevant test code and related helpers.
3. Compare the failure against known stable patterns from good Playwright examples.
   Path: `skill-design-inputs/playwright-good/`
4. Decide whether the evidence is sufficient.
5. Only request browser evidence when logs and code are not enough.

## Current limitation

This first version is intentionally conservative because failure examples may still be incomplete.
Until more examples arrive:
- avoid narrow heuristics;
- bias toward transparent uncertainty;
- keep repair permission strict.
