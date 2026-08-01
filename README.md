# Relex × Gemini

Let a lawyer's **Gemini** operate inside a **Relex** legal case — **without ever
receiving PII**.

> Relex doesn't replace Gemini. It helps you use Gemini end-to-end by protecting
> your PII data and know-how, automating customer service, handling payments for
> free, and giving you access to a new market. See
> [`docs/positioning.md`](docs/positioning.md).

Downstream of the shared Relex MCP server. Base package:
[relexyou/relex-mcp](https://github.com/relexyou/relex-mcp). Sibling connectors:
[Claude](https://github.com/relexyou/relex-claude) ·
[GPT](https://github.com/relexyou/relex-gpt) ·
[Grok](https://github.com/relexyou/relex-grok).

## Official Google / Gemini names

| Surface | Product calls it |
|---------|------------------|
| **Gemini CLI** | **MCP server** (`gemini mcp add`, `mcpServers` in settings) |
| **Gemini Enterprise** | **Custom MCP Server** (data store / connector) |
| Personal Gemini web chat | Usually **no** arbitrary custom MCP — use CLI or Enterprise |

Always name **`relex`**, URL `https://relex.legal/api/mcp` (Streamable HTTP).

## How it works

Gemini connects over **Streamable HTTP** MCP. Tools: `search`, `execute`.
Auth: **`/mcp auth relex`** (browser OAuth) on CLI, or **API key** / Enterprise
IdP wiring as configured by admin.

## Quick start — Gemini CLI

```bash
gemini mcp add --transport http relex https://relex.legal/api/mcp
```

List status:

```bash
gemini mcp list
```

Authenticate when prompted:

```text
/mcp auth relex
```

Then say:

> Set up my practice workflow with Relex

### settings.json equivalent

User config `~/.gemini/settings.json` or project `.gemini/settings.json`:

```json
{
  "mcpServers": {
    "relex": {
      "httpUrl": "https://relex.legal/api/mcp"
    }
  }
}
```

With API key:

```json
{
  "mcpServers": {
    "relex": {
      "httpUrl": "https://relex.legal/api/mcp",
      "headers": {
        "Authorization": "Bearer rlx_..."
      }
    }
  }
}
```

> Tip: avoid underscores in the server name (`relex` is good; `relex_legal` can
> break some Gemini policy FQN parsers).

## Personal vs Team / Enterprise

| Plan / product | Who installs | Who connects |
|----------------|--------------|--------------|
| **Gemini CLI (personal)** | You run `gemini mcp add` | You complete `/mcp auth` / OAuth |
| **Gemini Enterprise / Google Cloud** | **Admin** registers a Custom MCP Server / data store for the org application | Members use the app; OAuth or IdP as configured by admin |

### Gemini Enterprise (admin)

1. Deploy or point at the **hosted** Relex URL (no need to re-host unless
   required by network policy): `https://relex.legal/api/mcp`.
2. In Gemini Enterprise / Agent Builder, add a **Custom MCP Server** connector
   with that URL.
3. Configure OAuth / IdP per Google’s custom MCP docs.
4. Publish the application so members can use Relex tools.

Members typically **cannot** register arbitrary custom MCP servers themselves
in a managed Enterprise tenant — same pattern as Claude Team and ChatGPT
Enterprise.

Full guide: [`docs/install.md`](docs/install.md) ·
[`docs/connect-gemini-cli.md`](docs/connect-gemini-cli.md) ·
[`docs/connect-gemini-enterprise.md`](docs/connect-gemini-enterprise.md).

## Layout

```
relex-gemini/
├── plugin/
│   ├── .mcp.json
│   ├── plugin.json
│   ├── skills/
│   ├── agents/
│   ├── commands/
│   └── references/
├── docs/
│   ├── install.md
│   ├── connect-gemini-cli.md
│   ├── connect-gemini-enterprise.md
│   └── positioning.md
└── SECURITY.md
```

## Docs on relex.legal

- [Gemini connector](https://relex.legal/docs/connectors/gemini)
- [MCP Server](https://relex.legal/docs/mcp)
- [For AI Agents](https://relex.legal/for-agents)

## License

AGPL-3.0-or-later — see [LICENSE](LICENSE).
