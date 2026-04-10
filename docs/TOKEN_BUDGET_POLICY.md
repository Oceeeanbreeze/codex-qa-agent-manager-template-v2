# Token Budget Policy

## Goal

Prevent wasteful Codex usage so the team does not burn through limits during routine QA work.

## Default model policy

Use `gpt-5.4-mini` by default for:
- routing
- research
- testcase generation
- Playwright generation
- failure triage
- browser evidence summaries
- archival

Use `gpt-5.4` only when:
- requirements are ambiguous
- the failure has multiple plausible root causes
- the repair has high regression risk
- reviewer judgment requires deeper reasoning

## Spawn policy

- default maximum active subagents per task: `2`
- default maximum depth: `1`
- do not spawn specialist agents unless the router can justify them
- do not spawn browser work unless there is a UI-evidence trigger

## Retrieval policy

- retrieve from one scoped folder first
- do not retrieve the full memory corpus
- summarize large logs before triage
- never send raw bulk artifacts to every stage

## Cost-saving hard rules

- no browser validation by default
- no full-vault retrieval by default
- no automatic archival of intermediate reasoning
- no heavy model escalation for routine Playwright updates
- no repair before triage

## Weekly survivability rule

If the team starts to approach usage limits:
- disable non-essential browser runs
- disable broad reviewer passes on low-risk testcase generation
- keep triage-first intact
- keep reviewer mandatory for repairs and new automation
