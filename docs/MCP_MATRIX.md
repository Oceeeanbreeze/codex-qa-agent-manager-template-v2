# MCP Matrix

## Current state

As of April 10, 2026, the V2 repository itself does not include any active external MCP server registrations.

This means:
- the workflow can already run on built-in Codex capabilities such as local shell, filesystem access, browser tooling, and web access when available in the operator environment;
- GitHub MCP and OpenAI docs MCP are recommended next-step integrations, but they still require local Codex-side setup and approval.

## QA Team Mode

| MCP or capability | Why it is needed | Who needs it | Required or optional |
| --- | --- | --- | --- |
| Local shell and filesystem | Read repo files, run scripts, execute tests, patch code, validate fixes | router, researcher, test-automation-engineer, reviewer | Required |
| Browser automation and evidence | Reproduce UI failures, inspect selectors, confirm auth and route issues | qa-browser, failure-triager | Required for UI-focused work |
| GitHub MCP | Read PR context, attach failure dossiers to issues or PRs, keep repair flow linked to repo work | reviewer, test-automation-engineer, developer operators, QA leads | Optional at bootstrap, recommended later |
| OpenAI docs MCP | Check current official Codex, subagent, skills, and model guidance | architect, router, repository maintainers | Optional at bootstrap, recommended later |
| Ticketing or test-management MCP | Link scenario packs, failures, and repairs to Jira, TestRail, or internal work items | QA leads, archivist, reviewer | Optional |

## Developer Triage Mode

| MCP or capability | Why it is needed | Who needs it | Required or optional |
| --- | --- | --- | --- |
| Local shell and filesystem | Read failure logs, inspect tests, patch failing specs, rerun validation | researcher, failure-triager, test-automation-engineer, reviewer | Required |
| Browser automation and evidence | Confirm selector drift, auth issues, and UI regressions only when triage needs live evidence | qa-browser, failure-triager | Optional by trigger, but strongly recommended |
| GitHub MCP | Read PR or branch context, comment triage results, link the fix back to developer workflow | reviewer, test-automation-engineer, developer operator | Optional, recommended |
| OpenAI docs MCP | Keep the developer loop aligned with current Codex behavior and model policy | repository maintainers, advanced operators | Optional |
| Ticketing or test-management MCP | Needed only if the developer loop must publish results outside GitHub | team leads, QA coordinators | Optional |

## Rule

Do not treat every useful integration as mandatory.
For V2, add an MCP only when it materially improves one of these:
- failure diagnosis quality;
- repair quality;
- artifact delivery;
- operational traceability;
- long-term maintainability of the agent system.
