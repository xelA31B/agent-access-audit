---
name: access-hardening
description: >
  This skill should be used when the user asks to "fix my agent permissions", "lock down Claude Code",
  "apply least privilege to my AI agents", "secure my MCP servers", "add deny rules for secrets",
  "harden my AI coding setup", or after an access-audit when the user wants the recommended fixes applied.
  Also triggers on the same requests in Russian ("ограничь доступы агента", "закрой доступ к секретам")
  or Hungarian.
metadata:
  version: "0.1.0"
---

# Access Hardening

Apply least-privilege changes to AI agent configuration — safely, with a clear diff and user confirmation.

## Style and safety rules

- Language of the user's request. Concise, professional, no filler.
- **Show the diff, then ask.** Present every planned change as before/after per file and wait for explicit confirmation (all, some, none).
- **Back up first.** Copy each file to `<file>.bak-YYYYMMDD` before editing.
- Never open sensitive files or print secret values. Never move secret values yourself; tell the user which environment variable to create and where.
- Do not remove an MCP server, plugin or hook without asking — propose disabling first.
- If the project is a git repository, make changes on a branch `harden/agent-access` and commit there; never push without confirmation.

## Typical changes

1. **Deny rules for sensitive files:** block the agent from reading and editing `.env*` and key files.
2. **Replace wildcard command permissions** with a short allow list of commands the project needs (build, test, lint, git status/diff); keep everything else on "ask".
3. **Block destructive operations** without confirmation: recursive delete, force push, hard reset, publishing packages, production deploy commands.
4. **Turn off auto-approve / bypass defaults**; keep them available only for sandboxed environments.
5. **MCP servers:** pin package versions, remove unused servers, use HTTPS for remote servers, pass each server only the environment variables it needs, move inline secrets to environment variables.
6. **Hooks and marketplaces:** disable hooks without a clear purpose; remove marketplaces from unknown sources.
7. **Git hygiene:** add `.env*` and local settings files to `.gitignore`.
8. **Instruction files:** remove instructions that disable confirmations or widen access.

## Report

```
**Applied:** N changes in M files (branch: harden/agent-access)
| File | Change | Risk removed |

**Skipped (needs your decision):** …
**Your next step:** e.g. set variable X in your shell profile / secret manager; restart the agent
```

Offer to re-run `access-audit` to confirm the new verdict and update the baseline.

## Branded document

Start the deliverable with a header block, translated into the document language: plugin name with ✦, document title, then subject · version · date · owner · status (draft or current). Follow with a 2–3 line summary and numbered sections; use tables for structured content and code blocks for anything to paste.

If the environment can render HTML artifacts or files, present it as a static HTML page (no scripts) in the house style: header band with a navy #1C1E4E to teal #0E7480 gradient and white text, meta details as small rounded pills, light background #F6F7FB, white rounded cards with a #E3E6EF border, summary card with a gold #FFC448 left accent, dark code blocks. Otherwise deliver the same structure as a document artifact or markdown.
