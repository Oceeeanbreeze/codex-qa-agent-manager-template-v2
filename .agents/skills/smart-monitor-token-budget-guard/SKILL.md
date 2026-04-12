---
name: smart-monitor-token-budget-guard
description: Use when planning or running Smart Monitor QA workflows and token waste must stay low. Best for keeping routing cheap, reducing unnecessary retrieval, and preventing overuse of browser runs, heavy models, or extra subagents.
---

# Smart Monitor Token Budget Guard

Keep Smart Monitor workflows cheap by default.

## Use this skill when

- choosing a pipeline;
- deciding whether another subagent is justified;
- deciding whether browser evidence is worth the cost;
- deciding whether a heavier model is truly needed.

## Default policy

- Prefer `gpt-5.4-mini` by default.
- Escalate only on ambiguity, high-risk reasoning, or reviewer-grade decisions.
- Keep the default pipeline narrow.
- Summarize large logs before deeper reasoning.
- Retrieve only from the smallest relevant memory scope.

## Hard rules

- Do not spawn subagents just because they exist.
- Do not run browser checks by default.
- Do not retrieve broad team memory when project-local evidence is enough.
- Do not carry raw logs into every stage.
- Do not call a repair agent before failure triage.

## Decision guide

Ask these in order:

1. Can the task be solved by one narrow agent?
2. Is browser evidence really required?
3. Is the current evidence already enough for a decision?
4. Would a more expensive model materially change the outcome?
5. Can the output be a compact artifact instead of a long chain of reasoning?

## Preferred outcomes

- fewer active agents;
- smaller context per stage;
- compact artifacts;
- explicit uncertainty instead of expensive over-analysis.
