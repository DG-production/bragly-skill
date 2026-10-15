# Bragly for AI agents

Manage your [Bragly](https://bragly.io) social proof from your AI assistant: triage reviews, report on NPS and sentiment, and build walls of love.

This repo has two parts, both built on open standards:

- **Bragly MCP server**: `https://app.bragly.io/api/mcp`. Reviews, tags, NPS, analytics, forms, widgets, walls of love and brand kit, behind Bragly sign-in (OAuth).
- **Skills** (`skills/`): [Agent Skills](https://agentskills.io) that chain those tools into complete workflows.

## Claude Code and Cowork

```
/plugin marketplace add dg-production/bragly
/plugin install bragly@bragly
```

The first time Claude uses a Bragly tool it asks you to sign in. If it doesn't, run `/mcp`, pick `bragly` and choose Authenticate. Claude only sees the teams you belong to.

## Other agents

Any agent that supports remote MCP servers and Agent Skills can use Bragly:

1. Add the MCP server `https://app.bragly.io/api/mcp` (HTTP transport) and sign in when prompted.
2. Copy the folders in `skills/` into your agent's skills directory.

## Skills

| Skill | What it does |
| --- | --- |
| `review-triage` | Classifies sentiment, tags recurring themes and flags negative reviews for follow-up. Hides reviews only after you confirm. |
| `insights-report` | NPS, ratings, sources and traffic compared with the previous period, plus themes and ready-to-use quotes. Read-only. |
| `wall-of-love-builder` | Creates a wall of love from your best reviews and returns the public and edit links. |

Ask in plain language, e.g. "triage my reviews from this month" or "give me an NPS report for Q3".

## Development

```
claude --plugin-dir .
claude plugin validate .
```

To test against a local Bragly app, point `.mcp.json` at `http://localhost:3000/api/mcp`.

## Repository layout

```
skills/            # Agent Skills, shared by every agent
.mcp.json          # MCP server config (Claude)
.claude-plugin/    # Claude plugin manifest and marketplace
logo.png
```

Manifests for other agents go beside `.claude-plugin/` and reuse `skills/` and the same MCP URL.

## Support

[bragly.io/contact](https://bragly.io/contact) · [Privacy](https://bragly.io/privacy-policy) · [Terms](https://bragly.io/terms-of-service)

## License

MIT
