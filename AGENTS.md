# Smart Monitor Agent System V2

## Goal

Turn this repository into a Codex-native Smart Monitor QA system that can:
- write regulated testcases;
- write and update Playwright autotests;
- analyze failed tests;
- propose and implement safe test repairs after triage.

## Non-goals

This system must not:
- auto-fix tests before failure triage is complete;
- use broad memory retrieval across all folders by default;
- use high-cost reasoning models for routine work;
- archive every intermediate thought into durable memory;
- treat raw logs or raw traces as team memory.

## Agent set

### Required working agents
- `router`
- `researcher`
- `scenario-designer`
- `test-automation-engineer`
- `failure-triager`
- `qa-browser`
- `reviewer`

### Service agent
- `archivist`

## Why the system is split

The system is intentionally split into small agents because:
- routing, research, scenario design, failure diagnosis, browser evidence, code generation, and review are different reasoning modes;
- smaller agents reduce context pollution;
- smaller agents reduce accidental overreach and unnecessary writes;
- smaller agents allow cheaper routing and better token control;
- smaller agents are easier to evaluate separately.

Do not collapse these roles into one universal agent.

## Stage ownership

- `router`: selects the smallest safe pipeline
- `researcher`: gathers facts from code, tests, helpers, and known artifacts
- `scenario-designer`: writes regulated manual scenarios
- `test-automation-engineer`: writes or updates Playwright tests
- `failure-triager`: explains why a test failed before any repair proposal
- `qa-browser`: gathers browser-only evidence when UI evidence is required
- `reviewer`: validates quality, regression safety, and missing checks
- `archivist`: stores approved artifacts and known reusable knowledge

## Pipeline rules

### Testcase generation
- `router -> researcher -> scenario-designer -> reviewer -> archivist`

### Automation generation
- `router -> researcher -> test-automation-engineer -> reviewer -> archivist`

### Failure analysis
- `router -> researcher -> failure-triager -> qa-browser if needed -> reviewer -> archivist`

### Test repair
- `router -> failure-triager -> test-automation-engineer -> reviewer -> qa-browser or tester if needed -> archivist`

## Hard rules

- Never skip `failure-triager` before proposing a fix for a failed test.
- Never run `qa-browser` by default; use it only when UI evidence is required.
- Never use `archivist` for transient notes.
- Never retrieve the full shared vault when one scoped folder is enough.
- Never let one subagent own multiple unrelated responsibilities.

## Required outputs by stage

- `scenario-designer` -> `scenario-pack`
- `test-automation-engineer` -> `automation-spec` or code patch
- `failure-triager` -> `failure-dossier`
- `reviewer` -> findings or explicit pass with residual risk
- `archivist` -> approved durable note or no-op

## Failure categories

Every failure triage must classify the failure into one of:
- `selector-drift`
- `auth-or-stand`
- `timing-or-flake`
- `test-data`
- `test-bug`
- `product-bug`
- `unknown`

The triage output must include confidence and evidence.

## Memory rules

- Shared memory is markdown only.
- Indexes are local caches and must be rebuildable.
- Archive only approved artifacts, recurring patterns, and stable known issues.
- Do not store secrets, tokens, raw auth data, HAR files, or raw traces in durable memory.

## Token rules

- Default model family for routine work: `gpt-5.4-mini`
- High-cost reasoning is allowed only for ambiguous or high-risk cases.
- Max subagents per task by default: `2`
- Max depth: `1`
- Retrieve only the smallest relevant memory scope.

## Definition of done

The system is not done when it only returns text in chat.
The system is done only when it produces the required artifact for the stage and clearly states:
- outcome;
- evidence used;
- residual risk;
- whether anything was archived.
