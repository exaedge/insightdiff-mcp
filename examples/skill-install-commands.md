# Skill Install Commands

The InsightDiff MCP skill is optional. It gives supported AI agents workflow
rules, tool usage guidance, and troubleshooting notes for InsightDiff MCP.

The skill source is committed in this repository at `skills/insightdiff-mcp`.
Clone the repo and copy that folder into the skill directory for your agent.

Claude Code:

```bash
git clone https://github.com/exaedge/insightdiff-mcp.git
mkdir -p ~/.claude/skills
cp -R insightdiff-mcp/skills/insightdiff-mcp ~/.claude/skills/
```

OpenCode:

```bash
git clone https://github.com/exaedge/insightdiff-mcp.git
mkdir -p ~/.opencode/skill
cp -R insightdiff-mcp/skills/insightdiff-mcp ~/.opencode/skill/
```

Cursor:

```bash
git clone https://github.com/exaedge/insightdiff-mcp.git
mkdir -p ~/.cursor/skills
cp -R insightdiff-mcp/skills/insightdiff-mcp ~/.cursor/skills/
```

Restart the agent or editor after installation.
