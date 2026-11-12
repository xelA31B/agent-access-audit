---
name: access-audit
description: >
  This skill should be used when the user asks "what can my AI agent access", "audit my Claude Code
  permissions", "are my MCP servers safe", "check agent permissions in this project", "security review
  of my AI coding setup", "which tools can Claude run here", "audit Cursor / Claude / Codex agent
  config", or wants a security assessment of AI agents, MCP servers, plugins and hooks configured on a
  project or machine. Also triggers on the same requests in Russian ("проверь доступы агента",
  "безопасны ли MCP-серверы", "аудит прав ИИ-агента") or Hungarian.
metadata:
  version: "0.1.0"
---

# Agent Access Audit

Show what AI agents configured for a project or machine can read, run, change and send — and which of it is risky.

## Style and safety rules

- Language of the user's request. Concise, professional, no filler. Tables over paragraphs.
- **Read-only.** Do not change any configuration during the audit. Fixes are offered afterwards (`access-hardening`).
- **Secrets:** never print a full key, token or password; show at most the first 4 characters and where it was found.
- Report only what you actually read. Mark files that do not exist as **not present** and files you could not open as **not checked**.

## Step 1 — Scope

Default scope: the current project folder plus user-level agent configuration if accessible. Ask only if unclear: which project(s), and which agents are in use (Claude Code, Claude Desktop/Cowork, Cursor, VS Code Copilot agents, Windsurf, Codex, Gemini CLI).

## Step 2 — Collect configuration

Read the files listed in `references/config-locations.md` that exist. For each agent, build an inventory:

- **Permissions:** allow / ask / deny rules, default mode, bypass or auto-approve settings
- **MCP servers:** name, transport (local command or remote URL), command and arguments, source/package, version pinning, environment variables (names only), scope (project/user)
- **Hooks:** event, command, what it can do
- **Plugins and marketplaces:** enabled plugins, marketplace sources
- **Instruction files:** CLAUDE.md, AGENTS.md, rules files — instructions that widen access or disable confirmations
- **Exposed secrets reachable by the agent:** `.env` and similar files, keys inline in config, whether they are git-ignored

## Step 3 — Assess risk

Use the rubric in `references/risk-rubric.md`. Rate each finding **Critical / High / Medium / Low** and explain the concrete consequence in one plain sentence (e.g. "any MCP tool can read your AWS keys").

## Step 4 — Report

```
# Agent Access Audit — [project] · [date]

**Verdict:** 🟢 Safe / 🟡 Review needed / 🔴 Risky — one-line reason

## What your agents can do
| Agent | Read files | Write files | Run commands | Network | Secrets reachable |
(✅ limited · ⚠️ broad · ❌ none · ? not checked)

## Findings
| # | Severity | Finding | Consequence | Fix | Where |

## Inventory
| Type | Name | Source | Scope | Notes |
(MCP servers, hooks, plugins, marketplaces)

## Not checked
- item — what is needed
```

Verdict rule: 🔴 if any Critical finding; 🟡 if any High; otherwise 🟢.

## Step 5 — Baseline

Offer to save the result as `AGENT_ACCESS_BASELINE.md` in the project root (ask first; secrets masked) so the next run can show only what changed (`access-drift`). Recommend re-running after adding any MCP server, plugin or hook, and monthly.

Close with one line offering to apply fixes with `access-hardening`.

## Recurring run

At the end of the report, offer a recurring run. Recommended cadence: weekly drift check (access-drift), plus right after adding any MCP server, plugin or hook.

Let the user choose their own schedule. Ask in one short message, with the recommendation pre-filled:

- **Frequency:** daily · weekly · every 2 weeks · monthly · quarterly · custom
- **Day:** e.g. Monday, Friday, 1st of the month
- **Time and time zone:** e.g. 09:00 Europe/Budapest (use the user's time zone if known)
- **Delivery:** in this chat, a new chat, or a document

If the environment offers scheduled tasks (a scheduling tool is available), create the task only after the user confirms these choices. Write the scheduled prompt so it is self-contained: what to check (project, repository or company), which skill to run, the report language, and where to deliver the result. Confirm what was scheduled in one line. The user can change or cancel the schedule at any time; when asked, update or remove it.

If no scheduling tool is available, state the chosen or recommended cadence and suggest a calendar reminder.
