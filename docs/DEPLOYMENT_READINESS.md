# Deployment Readiness

## Goal

Define when V2 is ready for a new Codex chat and test deployment.

## Minimum readiness checklist

The repository is ready for a test deployment only if all of these are true:

1. Native subagents exist in `.codex/agents/`.
2. Repo-scoped skills exist in `.agents/skills/`.
3. `AGENTS.md` and `docs/CODEX_BOOTSTRAP_PROMPT.md` are aligned with the current repository layout.
4. Testcase regulation exists and is readable.
5. Memory policy exists.
6. Token budget policy exists.
7. MCP expectations are documented.
8. At least one seed set of manual testcase artifacts exists.
9. The repository does not contain secrets, raw auth data, traces, or runtime artifacts.

## Shared memory readiness

Shared memory is preferred, but it is not a hard blocker for the first deployment.

If shared memory is not ready yet:
- continue in local-only mode;
- skip shared retrieval;
- do not block testcase generation, automation generation, failure triage, or repair workflow setup;
- archive only into local or repository-safe draft artifacts.

## First deployment mode

The first deployment should be treated as a controlled test deployment, not full production rollout.

Recommended scope:
- one module at a time;
- narrow tasks first;
- no broad browser fan-out;
- no bulk archival;
- triage-first on failures.

## Ready / not ready rule

V2 is ready for a new bootstrap chat when:
- the readiness checklist passes;
- the operator understands that shared memory may still be local-only at first;
- the deployment goal is a test rollout, not final production scale.
