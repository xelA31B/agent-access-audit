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
- Read-only. Never open sensitive files or print secret values.

## Steps

1. **Load the baseline** `AGENT_ACCESS_BASELINE.md`. If none exists, run `access-audit` instead and offer to save a baseline.
2. **Collect the current configuration** exactly as `access-audit` does.
3. **Diff** by category: permissions, MCP servers, hooks, plugins and marketplaces, instruction files, sensitive-file protection.
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

## Branded report

If the environment can render HTML artifacts or files, present the full report as a static HTML page (no scripts) in the house style below; otherwise use the markdown format above. Keep the chat reply to a short summary either way.

House style:
- Header band with a diagonal gradient from deep navy #1C1E4E to teal #0E7480, white text: small uppercase plugin name with a gold ✦ (#FFC448), the report title, then subject and date.
- Light background #F6F7FB; content in white cards with a thin #E3E6EF border and rounded corners (about 16 px).
- Summary card first: a circular score ring (teal arc proportional to the score, number in the centre in navy), the verdict and 2–3 key points.
- Status chips as small rounded labels: green #1F9D63 pass, amber #E0A000 warning, red #D64545 fail, grey #8A90A2 not checked.
- Tables with muted header text #5B6275 and thin row lines; evidence in small monospace.
- Footer line with the plugin name.

## Recurring run

At the end of the report, offer a recurring run. Recommended cadence: weekly, plus right after adding any MCP server, plugin or hook.

Let the user choose their own schedule. Ask in one short message, with the recommendation pre-filled:

- **Frequency:** daily · weekly · every 2 weeks · monthly · quarterly · custom
- **Day:** e.g. Monday, Friday, 1st of the month
- **Time and time zone:** e.g. 09:00 Europe/Budapest (use the user's time zone if known)
- **Delivery:** in this chat, a new chat, or a document

If the environment offers scheduled tasks (a scheduling tool is available), create the task only after the user confirms these choices. Write the scheduled prompt so it is self-contained: what to check (project, repository or company), which skill to run, the report language, and where to deliver the result. Confirm what was scheduled in one line. The user can change or cancel the schedule at any time; when asked, update or remove it.

If no scheduling tool is available, state the chosen or recommended cadence and suggest a calendar reminder.
