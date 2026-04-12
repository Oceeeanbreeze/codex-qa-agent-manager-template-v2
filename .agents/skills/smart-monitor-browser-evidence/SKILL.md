---
name: smart-monitor-browser-evidence
description: Use when Smart Monitor failure triage needs live UI evidence before a safe conclusion can be made. Best for confirming selector drift, route issues, auth problems, modal behavior, and visible regressions without jumping straight to code fixes.
---

# Smart Monitor Browser Evidence

Collect browser-only evidence for Smart Monitor UI failures.

## Use this skill when

- failure triage says logs and code are not enough;
- the likely problem is selector drift, auth-or-stand, route navigation, modal state, or visible UI regression;
- the next decision depends on what the UI actually does at runtime.

## Main goal

Return evidence, not a speculative fix.

## Required output

Produce a compact browser-evidence note with:
- route or page checked;
- visible state observed;
- exact action that reproduced the issue;
- selector or UI signal involved;
- whether the result supports `product-bug`, `test-bug`, `selector-drift`, `auth-or-stand`, or `unknown`;
- whether repair should proceed or stop.

## Hard rules

- Do not propose code fixes by default.
- Do not run a full exploratory session.
- Check one main happy path and one relevant failure path only.
- Prefer project-standard routes and helper logic when known.
- Call out if the only available locator is weak or localization-dependent.
- If the page is blocked by auth or stand instability, say so directly.

## Workflow

1. Start from the triaged failure context.
2. Reproduce only the smallest path needed to confirm or reject the hypothesis.
3. Record what is visible and observable.
4. Separate:
   - selector issue;
   - auth or stand issue;
   - product regression;
   - unknown.
5. Hand back a recommendation for the next stage:
   - stop at dossier;
   - request product fix;
   - allow test repair.

## Smart Monitor-specific rules

- Prefer route checks that match existing repository flows.
- Prefer `data-test-subj` based evidence when available.
- If the UI path still depends on localized text or CSS fallbacks, mark that as selector debt.
- Reuse known helper behavior conceptually:
  - app route opening;
  - loader wait;
  - auth guard;
  - fatal app error guard.

## When not to use this skill

Do not use it when:
- failure logs already prove the cause;
- the task is only testcase authoring;
- the repair can already be justified from code and dossier evidence without UI confirmation.
