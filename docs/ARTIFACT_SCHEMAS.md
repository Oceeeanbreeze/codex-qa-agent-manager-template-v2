# Artifact Schemas

## Goal

Make every stage output explicit and reviewable.

The system should not treat "a chat answer" as a sufficient stage result.

## `scenario-pack`

Minimum required fields:
- `id`
- `title`
- `product`
- `module_path`
- `component`
- `priority`
- `type`
- `status`
- `description`
- `preconditions`
- `test_data`
- `steps_table`
- `postconditions`
- `automation`

Primary format:
- YAML

## `automation-spec`

Minimum required fields:
- source scenario or testcase id
- target file or proposed file name
- scope of automation
- selectors strategy
- helper reuse plan
- assertions plan
- setup and cleanup assumptions
- browser compatibility notes
- residual risks

Primary format:
- markdown or YAML

## `failure-dossier`

Minimum required fields:
- failing test name
- failure category
- product-side or test-side decision
- confidence
- evidence used
- likely root cause
- open uncertainty
- browser evidence required: yes or no
- repair allowed: yes or no

Primary format:
- markdown or YAML

## `repair-report`

Minimum required fields:
- source failure category
- summary of repaired issue
- changed files
- why this fix matches the triage
- residual risks
- follow-up checks

Primary format:
- markdown

## Rule

If a stage cannot produce its full artifact yet, it must still return:
- the partial artifact;
- what is missing;
- what evidence blocked completion.
