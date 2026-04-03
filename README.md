# product-research-skill

A Claude Code plugin for structured product benchmark research. Analyzes multiple competing services and produces a comprehensive Notion page with per-service deep dives, common feature patterns, gap analysis, and strategic positioning.

## What it does

1. **Discovers** 6–10 relevant services for your research topic
2. **Analyzes** each service — features, UX, pricing, user reviews
3. **Synthesizes** cross-service patterns, gaps, and strategic implications
4. **Documents** everything in a structured Notion page (auto-created)

## Installation

```
/install-github-plugin sonya/product-research-skill
```

> Requires Claude Code with Notion MCP configured.

## Usage

```
/product-research AI interview tools
/product-research note-taking apps for developers
/product-research B2B onboarding automation
```

## Skills

| Skill | Trigger | Description |
|-------|---------|-------------|
| `product-research` | `/product-research [topic]` | Main skill — orchestrates the full research flow |
| `product-research-service` | Internal | Analyzes one service and writes to Notion |
| `product-research-synthesis` | Internal | Cross-service patterns, gaps, positioning |

## Notion Page Structure

Each research session creates a Notion page with:

- **분석 대상 서비스** — checklist tracking per-service completion
- **개별 툴 분석** — per-service sections with features (toggles + screenshots), UX notes, user reviews, and competitive positioning callout
- **공통 기능 패턴** — frequency-ranked feature pattern table with category tags
- **공백(Gap) 패턴** — features not yet built by anyone (opportunity map)
- **시사점 & 포지셔닝** — 2×2 competitive map + strategic implications

## Requirements

- Claude Code
- Notion MCP server configured (`mcp__notion__*` or `mcp__claude_ai_Notion__*`)

## License

MIT
