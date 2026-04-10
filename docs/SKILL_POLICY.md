# Skill Policy

## Goal

Define which skills from the old system can be reused, which must be adapted, which should be excluded, and which new skills must exist in Smart Monitor Agent System V2.

## Core rule

Do not move the old skill pack into V2 unchanged.

V2 uses a narrower architecture:
- fewer active agents per task;
- triage before repair;
- Playwright-first automation;
- markdown artifacts instead of broad conversational outputs;
- explicit token-budget control.

Repo-scoped skills for V2 should ultimately live in `.agents/skills`.
Use this document as the migration policy for old skills.

## Status definitions

- `carry`: can be migrated with only light wording cleanup
- `adapt`: useful core, but the scope or output must be rewritten for V2
- `drop`: do not migrate into V2
- `new`: create specifically for V2

## Old skill inventory review

### Carry

These skills are already narrow, high-signal, and aligned with the new architecture.

#### `atomic-testcase-writer`
Status: `carry`

Why:
- already matches one goal per case and one action per step
- already aligns with Smart Monitor manual-case writing
- already pushes observable expected results

Use in V2:
- primary skill for `scenario-designer`

Needed changes:
- light wording cleanup only
- make the required output explicitly `scenario-pack`

#### `playwright-e2e-builder`
Status: `carry`

Why:
- already enforces focused Playwright tests
- already promotes helper reuse and deterministic checks
- already discourages timing anti-patterns

Use in V2:
- base automation-writing skill for `test-automation-engineer`

Needed changes:
- light wording cleanup only
- make output explicitly compatible with `automation-spec`

#### `playwright-review-checklist`
Status: `carry`

Why:
- strong review checklist for browser automation
- useful as a quality gate after generation or repair
- maps directly to the `reviewer` role

Use in V2:
- secondary review skill for `reviewer`

Needed changes:
- no architectural change
- keep as a reviewer-only skill

#### `regression-hunter`
Status: `carry`

Why:
- still valuable in V2 as the generic regression lens
- complements Playwright-specific review

Use in V2:
- core review skill for `reviewer`

Needed changes:
- none beyond wording cleanup

#### `test-surface-finder`
Status: `carry`

Why:
- useful for locating affected feature surfaces before testcase writing or automation
- narrow and evidence-oriented

Use in V2:
- primary research skill for `researcher`

Needed changes:
- no major change

### Adapt

These skills are valuable, but their old scope is broader than what V2 should allow.

#### `agent-browser`
Status: `adapt`

Why:
- good at page and DOM analysis
- too broad in its current form for the new browser-evidence policy

Problem in old form:
- mixes page analysis, scenario extraction, automation suggestions, and HTML intake in one skill
- risks encouraging browser exploration too early

V2 target:
- rewrite into a narrower browser-evidence skill for `qa-browser`
- use only when the pipeline has a UI-evidence trigger

#### `browser-qa-playbook`
Status: `adapt`

Why:
- solid browser validation workflow
- needs tighter trigger rules and output schema

Problem in old form:
- exploratory QA can become default behavior

V2 target:
- use only after `failure-triager` or when explicitly requested
- output must map into `failure-dossier` evidence

#### `smart-monitor-feature-analysis`
Status: `adapt`

Why:
- useful Smart Monitor domain analysis
- should be preserved as a domain-anchoring skill

Problem in old form:
- overlaps with general research and test-surface discovery

V2 target:
- keep only Smart Monitor-specific logic
- remove generic research duties already handled by `researcher`

#### `requirements-extractor`
Status: `adapt`

Why:
- still useful for ambiguous requests
- too generic to run on every task by default

V2 target:
- reserve for `router` or `researcher` only when requirements are incomplete
- avoid using it in routine failure triage

#### `task-router-risk-triage`
Status: `adapt`

Why:
- routing logic is valuable
- the old route taxonomy is still too broad for the new stage-based pipeline

V2 target:
- rewrite around the V2 pipeline decisions:
  - testcase
  - automation
  - failure-analysis
  - repair

#### `risk-based-test-checklists`
Status: `adapt`

Why:
- useful for validation summaries
- too broad if treated as a default stage output

V2 target:
- keep as optional validation support
- not a primary artifact generator

#### `test-gap-audit`
Status: `adapt`

Why:
- useful for coverage review and future roadmap work
- not part of the minimal operational path

V2 target:
- use only for coverage planning or review-heavy tasks
- not in the default generation or triage flow

#### `vault-archivist`
Status: `adapt`

Why:
- strong note hygiene principles
- archive discipline is still needed

Problem in old form:
- still too general for a team-shared memory model

V2 target:
- rewrite around approved artifact-only archival
- align with shared markdown memory and local index policy

#### `test-hook-enabler`
Status: `adapt`

Why:
- still useful when selectors or seams block automation

Problem in old form:
- framed as a generic testability helper

V2 target:
- use only when triage proves the test is blocked by missing stable hooks
- make it subordinate to `failure-triager` and `test-automation-engineer`

### Drop

These skills are not wrong, but they are not part of the minimal V2 system and should not be migrated into the first release.

#### `api-integration-test-builder`
Status: `drop`

Why:
- backend and API automation are a future concern
- V2 is front-end and Playwright-first

Future note:
- may return in a later hybrid QA stack

#### `test-pyramid-planner`
Status: `drop`

Why:
- useful strategically, but adds abstraction and routing overhead
- not needed for the first Playwright-first version

#### `playwright-smart-monitor-writer`
Status: `drop`

Why:
- its useful parts should be merged into the new Playwright automation skill
- keeping both would duplicate responsibilities

#### `test-gap-audit` as default behavior
Status: `drop from default pipelines`

Why:
- valuable only as an optional audit tool
- too expensive to keep in the normal path

## New V2 skills

These skills should be created specifically for the new architecture.

### `smart-monitor-scenario-pack-writer`
Status: `new`

Purpose:
- generate regulated Smart Monitor testcase artifacts
- explicit output: `scenario-pack`

### `smart-monitor-playwright-automation-writer`
Status: `new`

Purpose:
- generate or update Playwright tests in the exact Smart Monitor house style
- explicit output: `automation-spec` and or code patch

Why new instead of reusing `playwright-smart-monitor-writer` unchanged:
- V2 needs token-budget policy and stricter output discipline
- V2 must separate generation from repair

### `smart-monitor-failure-triage`
Status: `new`

Purpose:
- classify failures into:
  - selector-drift
  - auth-or-stand
  - timing-or-flake
  - test-data
  - test-bug
  - product-bug
  - unknown
- explicit output: `failure-dossier`

### `smart-monitor-test-repair-policy`
Status: `new`

Purpose:
- define how a test may be repaired after triage
- forbid speculative fixes before diagnosis
- explicit output: `repair-report`

### `smart-monitor-browser-evidence`
Status: `new`

Purpose:
- narrow browser work to evidence collection
- prevent broad exploratory browser use by default

### `smart-monitor-memory-archival`
Status: `new`

Purpose:
- decide what approved knowledge enters shared markdown memory
- reject raw and sensitive artifacts

### `smart-monitor-token-budget-guard`
Status: `new`

Purpose:
- enforce the V2 budget rules:
  - mini by default
  - no broad retrieval
  - no unnecessary browser runs
  - no unnecessary parallel subagents

## Final migration decision

### Move into V2 now
- `atomic-testcase-writer`
- `playwright-e2e-builder`
- `playwright-review-checklist`
- `regression-hunter`
- `test-surface-finder`

### Move only after rewrite
- `agent-browser`
- `browser-qa-playbook`
- `smart-monitor-feature-analysis`
- `requirements-extractor`
- `task-router-risk-triage`
- `risk-based-test-checklists`
- `test-gap-audit`
- `vault-archivist`
- `test-hook-enabler`

### Do not include in V2 initial release
- `api-integration-test-builder`
- `test-pyramid-planner`
- the old standalone `playwright-smart-monitor-writer`

## Rule for implementation

Do not create every migrated skill on day one.

Build V2 in this order:
1. scenario writing
2. Playwright writing
3. failure triage
4. browser evidence
5. repair policy
6. archival policy
7. optional coverage and strategy skills
