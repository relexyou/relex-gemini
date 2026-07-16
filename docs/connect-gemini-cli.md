# Connect Relex to Gemini CLI

```bash
gemini mcp add --transport http relex https://relex.you/api/mcp
gemini mcp list
```

In an interactive session:

```text
/mcp
/mcp auth relex
```

Then:

> Set up my practice workflow with Relex

## Manual settings.json

```json
{
  "mcpServers": {
    "relex": {
      "httpUrl": "https://relex.you/api/mcp",
      "timeout": 60000
    }
  }
}
```

Scope: `-s user` for `~/.gemini/settings.json`, or project `.gemini/settings.json`.

## Remove

```bash
gemini mcp remove relex
```

## Skills

Point Gemini at `plugin/skills/relex/SKILL.md` (and siblings) for the full
deep-link-first practice workflow.
