---
name: access-drift
description: >
  This skill should be used when the user asks "what changed in my agent permissions", "re-check agent
  access", "compare with the last audit", "did my new MCP server add risk", "monthly agent security
  check", or when an AGENT_ACCESS_BASELINE.md file exists and the user wants an updated audit.
  Also triggers on the same requests in Russian ("что изменилось в доступах агента", "повторная проверка
  доступов") or Hungarian.
metadata:
  version: "0.1.0"
---

# Access Drift

Compare the current agent configuration with the saved baseline and report only what changed.

## Style and safety rules

- Language of the user's request. Concise, professional, no filler.
- Read-only. Secrets masked (first 4 characters at most).

## Steps

1. **Load the baseline** `AGENT_ACCESS_BASELINE.md`. If none exists, run `access-audit` instead and offer to save a baseline.
2. **Collect the current configuration** exactly as `access-audit` does.
3. **Diff** by category: permissions, MCP servers, hooks, plugins and marketplaces, instruction files, reachable secrets.
4. **Assess** each change with the `access-audit` risk rubric.
5. **Report:**

```
# Agent Access Drift — [project] · baseline [date] → now

**Verdict change:** 🟢 → 🟡 (reason)

## New or increased risk
| Severity | Change | Consequence | Fix |

## Reduced risk
- one line each

## Unchanged
- summary in one line

## Added / removed
| Type | Name | Added / Removed | Source |
```

6. **Offer** to update the baseline (ask first) and to fix new risks with `access-hardening`.

Suggest a routine: run after every new MCP server, plugin or hook, and monthly.

## Recurring run

Recommend a cadence at the end of the report: weekly, plus right after adding any MCP server, plugin or hook.
If the environment offers scheduled tasks (a scheduling tool is available), offer in one line to set one up, e.g. "every Monday at 09:00". Create it only after the user agrees and confirms day and time. Write the scheduled prompt so it is self-contained: what to check (project, repository or company), which skill to run, and where to deliver the result. If no scheduling tool is available, state the recommended cadence and suggest a calendar reminder.
