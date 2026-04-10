# MCP Strategy

## Goal

Document:
- which capabilities are already available to the current Smart Monitor workflows;
- which external MCP integrations are recommended next;
- how to avoid pretending a connector is active when it is not.

## Important distinction

V2 uses two layers:
- built-in Codex capabilities already available in the operator environment;
- external MCP servers or connectors that may be added later.

As of April 10, 2026, the repository does not include any active external MCP registrations by itself.
That means GitHub MCP and OpenAI docs MCP should currently be treated as recommended integrations, not as already-enabled repository features.

## Capabilities already expected by the current V2 architecture

### 1. Browser automation and browser evidence MCP

Purpose:
- run UI checks
- gather browser-only evidence
- reproduce selector, auth, and route problems
- support Playwright-oriented diagnosis

Why it matters:
- V2 is front-end and Playwright-first
- `qa-browser` is intentionally built around UI evidence triggers

Typical usage:
- reproduce a failed UI flow
- inspect selector stability
- confirm whether the issue is UI-only or environment-related

Status:
- expected in the working operator environment
- treated as a core runtime capability

### 2. Local shell and filesystem execution

Purpose:
- inspect repository files
- run local scripts
- run test commands
- apply test fixes
- validate results

Why it matters:
- `researcher`, `test-automation-engineer`, and `reviewer` all rely on controlled local execution
- local scripts remain the main runtime surface for memory, health checks, and repository operations

Status:
- expected in the working operator environment
- treated as a core runtime capability

## MCPs not required on day one, but strongly recommended later

### 3. GitHub MCP

Purpose:
- open issues from failure dossiers
- read PR context
- comment on fixes
- attach diagnosis to the right development object

Why add later:
- very useful once developer mode starts producing actionable triage reports
- not required for the first repository bootstrap

Current status:
- recommended
- not active by default in this repository
- requires local Codex-side MCP setup

### 4. OpenAI developer docs MCP

Purpose:
- retrieve current official Codex and model guidance
- check current subagent and skills behavior
- validate upgrade decisions against official docs

Why add later:
- useful for keeping the agent system current over time
- not required for core Smart Monitor workflows, but valuable for maintenance and architecture decisions

Current status:
- recommended
- not active by default in this repository
- requires local Codex-side MCP setup

### 5. Test management or ticketing MCP

Examples:
- Jira
- TestRail
- internal QA systems

Purpose:
- attach scenario packs and failure dossiers to work items
- keep triage and repair reports linked to operational processes

Why add later:
- helpful once the system is trusted and needs to integrate with the team's delivery process

Current status:
- optional
- not active by default in this repository

## MCPs intentionally not required at the start

### Shared vector database as an MCP

Why not required:
- V2 deliberately treats markdown as source of truth and indexes as local rebuildable caches
- shared vector state adds operational complexity too early

### Broad external integrations

Why not required:
- the first goal is a controlled, deterministic local workflow
- external integrations should be added only after the core failure-analysis and repair loop is stable

## Recommended rollout order

1. browser automation and evidence
2. local shell and filesystem execution
3. GitHub integration
4. OpenAI docs integration
5. ticketing and test-management integrations

## Rule

Do not add an MCP just because it exists.
Add it only when it materially improves one of these:
- failure diagnosis quality
- repair loop quality
- artifact delivery
- operational traceability
