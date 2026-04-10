# MCP Setup Notes

## Goal

Record what is already available in the current environment, what is not yet connected, and how to treat MCP rollout in V2.

## What is already available now

The current Codex environment used to build V2 already has access to:
- local shell execution;
- local filesystem access;
- browser tooling for UI investigation;
- web access when the operator environment permits it.

These are enough to bootstrap and run the core Smart Monitor workflows.

The global Codex config path is typically:
- `~/.codex/config.toml`

## What is not yet connected as an active MCP server

At the time of writing, the repository itself does not own external MCP registrations.
External MCP activation happens in the operator's global Codex environment.

In practical terms:
- GitHub MCP is not yet active in this workspace;
- OpenAI docs MCP has been added to the global Codex config and should become active after restarting Codex;
- ticketing and test-management MCPs are not yet active in this workspace.

## GitHub MCP

### Why to add it

- read issue and pull request context without leaving the workflow;
- attach triage findings to the correct code review object;
- reduce manual copy-paste between diagnosis and development flow.

### Status in V2

- recommended;
- not required for bootstrap;
- requires local Codex-side MCP setup outside repository files;
- not activated yet in the current environment because no GitHub PAT environment variable is present.

### Recommended Codex config

Add this to the global Codex config after a GitHub PAT is available:

```toml
[mcp_servers.github]
url = "https://api.githubcopilot.com/mcp/"
bearer_token_env_var = "GITHUB_PAT_TOKEN"
```

### Required local prerequisite

The local environment must expose:

```text
GITHUB_PAT_TOKEN
```

Use least-privilege scopes first and expand only if a GitHub tool fails due to permissions.

### Rule

Do not claim GitHub MCP is active unless the local Codex environment actually exposes it as an MCP server or connector.

## OpenAI docs MCP

### Why to add it

- keep Codex subagent, skills, and model policies current;
- verify architecture decisions against current official OpenAI guidance;
- reduce drift between repository instructions and live Codex behavior.

### Status in V2

- recommended;
- not required for day-one Smart Monitor workflows;
- requires local Codex-side MCP setup outside repository files;
- already added to the current global Codex config, but Codex should be restarted before expecting the connector to appear in-tooling.

### Current Codex config

The current global config now contains:

```toml
[mcp_servers.openaiDeveloperDocs]
url = "https://developers.openai.com/mcp"
```

### Rule

If OpenAI docs MCP is not active, use official OpenAI documentation through the available operator workflow and treat that as fallback research, not as MCP-backed retrieval.

## Practical rollout order

1. keep local shell and browser workflows stable;
2. restart Codex so the OpenAI docs MCP config can load;
3. activate GitHub MCP after exporting `GITHUB_PAT_TOKEN`;
4. activate ticketing or test-management MCPs only after the core failure loop is trusted.

## Important boundary

Repository files can document and standardize MCP expectations, but they do not themselves guarantee that a connector is active.
Actual MCP activation depends on the local Codex environment, installed connectors, and operator approval.
