# Privacy Policy — Agent Access Audit

_Last updated: 12 November 2026_

This plugin is a set of instructions (skills) that runs inside Claude. It has no servers of its own.

- **No data collection.** The plugin author does not receive, store or process your configuration, code or reports.
- **What Claude reads.** Within your Claude session, Claude reads agent configuration files in the projects and folders you give it access to. The plugin instructs Claude never to open sensitive files such as `.env` or key files (it only checks that they exist and are git-ignored) and never to print secret values. Processing happens under Anthropic's terms and privacy policy.
- **Files the plugin may create, only with your confirmation:** a baseline report (`AGENT_ACCESS_BASELINE.md`, no secret values) and backups of configuration files you agree to change. They stay in your project.
- **No storage elsewhere, no third parties, no tracking.**

Questions: https://github.com/xelA31B/agent-access-audit/issues
