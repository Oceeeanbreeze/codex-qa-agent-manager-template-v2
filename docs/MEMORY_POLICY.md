# Memory Policy

## Source of truth

Shared team memory must be markdown.

Use a shared folder, synced folder, or shared Obsidian vault as the team source of truth.
Indexes must remain local and rebuildable.

## Approved memory types

Store only:
- testcase standards
- approved scenario packs
- approved automation specs
- failure dossiers
- repair reports
- known issues
- reusable Smart Monitor QA patterns

## Forbidden memory types

Do not store:
- tokens
- cookies
- raw auth data
- HAR files
- raw traces
- raw screenshots with sensitive data
- full unfiltered logs
- transient reasoning

## Suggested shared folder structure

```text
Shared-QA-Vault/
  Standards/
  SmartMonitor/
    Scenarios/
    Automation/
    Failures/
    Repairs/
    Known-Issues/
```

## Retrieval rules

- retrieve only from the smallest relevant scope
- prefer project-specific folders before global shared folders
- do not search the full vault by default
- use archived artifacts before raw conversations

## Local cache rules

Each operator or corporate Codex account must keep a separate local cache store.

Shared:
- markdown source of truth

Local only:
- vector indexes
- lexical indexes
- sqlite stores
- temporary evidence
