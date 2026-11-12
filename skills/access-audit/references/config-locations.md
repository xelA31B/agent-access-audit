# Where agent configuration lives

Check the paths that exist. Paths change between versions; if web search is available and a path is missing, verify the current location in the agent's documentation.

## Claude Code

- Project: `.claude/settings.json`, `.claude/settings.local.json`
- User: `~/.claude/settings.json`
- MCP servers: `.mcp.json` (project), user-level MCP configuration in `~/.claude.json`
- Plugins: enabled plugins and marketplaces in settings files
- Hooks: `hooks` section in settings files; plugin `hooks/hooks.json`
- Instructions: `CLAUDE.md`, `.claude/CLAUDE.md`, `~/.claude/CLAUDE.md`
- Skills and agents: `.claude/skills/`, `.claude/agents/`

## Claude Desktop

- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

## Cursor

- Project: `.cursor/mcp.json`, `.cursor/rules/`, `.cursorrules`
- User: `~/.cursor/mcp.json`

## VS Code (Copilot agent mode and MCP)

- Project: `.vscode/mcp.json`, `.vscode/settings.json`
- Instructions: `.github/copilot-instructions.md`

## Windsurf

- User: `~/.codeium/windsurf/mcp_config.json`; rules in `.windsurfrules`

## Codex CLI

- User: `~/.codex/config.toml`; instructions in `AGENTS.md`

## Gemini CLI

- Project: `.gemini/settings.json`; user: `~/.gemini/settings.json`; instructions in `GEMINI.md`

## Sensitive files in the project (presence only)

- Check only whether files such as `.env`, `.env.*`, `*.pem` or `*.key` exist in the project folder and whether `.gitignore` covers them.
- Do not open, read or print these files. Do not look outside the project folder for sensitive files.
