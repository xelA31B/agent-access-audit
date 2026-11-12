# Agent Access Audit — Claude plugin

AI coding agents and MCP servers often get access to your files, terminal and secrets without anyone looking closely. Agent Access Audit shows exactly what they can do, what is risky and how to lock it down.

## Install

**Claude app (web, desktop):** Plugins → add a marketplace from a GitHub repository → `xelA31B/agent-access-audit` → install **Agent Access Audit**. Once approved in the Claude directory, search for **Agent Access Audit** in Plugins.

**Claude Code (VS Code or terminal):**

```
/plugin marketplace add xelA31B/agent-access-audit
/plugin install agent-access-audit@agent-access-audit
```

## Skills

| Skill | What you get |
|-------|--------------|
| **access-audit** | Read-only audit of permissions, MCP servers, hooks, plugins, instruction files and unprotected sensitive files. Verdict 🟢/🟡/🔴, findings by severity, full inventory. Optional baseline file. |
| **access-hardening** | Least-privilege fixes shown as a diff, applied only after confirmation, with backups and a separate git branch. |
| **access-drift** | Compares the current setup with the saved baseline and reports only what changed — run after every new MCP server, plugin or hook, and monthly. |

Covers Claude Code, Claude Desktop, Cursor, VS Code agents, Windsurf, Codex CLI and Gemini CLI configuration.

## How to use

Best in Claude Code with the project open.

- "What can my AI agents access in this project?"
- "Проверь доступы агентов и MCP-серверов в этом проекте"
- "Re-check agent access against the baseline"

## Principles

Read-only by default, never opens sensitive files or prints secrets, no change without your confirmation. Concise reports in the language of your request.

## License

MIT
