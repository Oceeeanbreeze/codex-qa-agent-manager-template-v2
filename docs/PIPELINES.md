# Pipelines

## Testcase Generation

Use:
- `router`
- `researcher`
- `scenario-designer`
- `reviewer`
- `archivist` only if the scenario is approved

Output:
- `scenario-pack`

## Automation Generation

Use:
- `router`
- `researcher`
- `test-automation-engineer`
- `reviewer`
- `archivist` only if the output is approved

Output:
- `automation-spec` and or code patch

## Failure Analysis

Use:
- `router`
- `researcher`
- `failure-triager`
- `qa-browser` only if UI evidence is required
- `reviewer`
- `archivist` only if the triage is approved

Output:
- `failure-dossier`

## Test Repair

Use:
- `router`
- `failure-triager`
- `test-automation-engineer`
- `reviewer`
- `qa-browser` only if verification requires browser evidence
- `archivist` only if the repair result is approved

Output:
- code patch
- `repair-report`

## Browser trigger rules

Run `qa-browser` only when one of these is true:
- the failure is likely selector-related
- the failure is likely auth or stand related
- the failure is UI-only and logs are insufficient
- the fix proposal needs browser confirmation

Do not run `qa-browser` by default.
