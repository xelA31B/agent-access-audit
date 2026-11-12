# Risk rubric

## Critical

- Permission checks disabled or bypassed for all actions (auto-approve everything, bypass mode as default)
- Unrestricted shell access combined with network access and sensitive files not protected by deny rules
- Secrets (API keys, tokens, passwords) written inline in agent or MCP configuration committed to git
- MCP server or hook that downloads and executes remote code at start, from an unpinned or unknown source
- Instructions in CLAUDE.md / AGENTS.md / rules telling the agent to skip confirmations for destructive actions

## High

- Wildcard allow rules for shell commands (any command allowed without asking)
- Write access to the whole home directory or system folders
- No deny rules for secret files (`.env`, keys, credentials)
- MCP servers from unverified publishers or personal forks; packages without version pinning
- Remote MCP servers over plain HTTP or with tokens in the URL
- Allowed destructive git or file operations without confirmation (force push, hard reset, recursive delete)
- Hooks that run commands on every tool call without clear purpose
- Plugin marketplaces added from unknown repositories

## Medium

- Broad read access outside the project folder
- Many MCP servers enabled that the project does not use
- Environment variables with secrets passed to all MCP servers instead of only the one that needs them
- `.env` present but not in `.gitignore`
- No project-level settings (relying only on user defaults)

## Low

- Outdated agent versions or plugins
- Missing documentation of which agents and servers the project uses
- Instruction files with vague or conflicting rules

## Writing a finding

- Consequence first, in plain words: what an attacker, a malicious package or a confused agent could do.
- Point to the exact file and key name; never include secret values.
- Give the smallest fix that removes the risk.
