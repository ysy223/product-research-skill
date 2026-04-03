# product-research-skill

A Claude Code plugin for structured product benchmark research. Analyzes multiple competing services and produces a comprehensive Notion page with per-service deep dives, common feature patterns, gap analysis, and strategic positioning.

## What it does

1. **Discovers** 6–10 relevant services for your research topic
2. **Analyzes** each service — features, UX, pricing, user reviews
3. **Synthesizes** cross-service patterns, gaps, and strategic implications
4. **Documents** everything in a structured Notion page (auto-created)

## Installation

Clone the repo and copy the skills to your Claude skills directory:

```bash
git clone https://github.com/ysy223/product-research-skill.git
cp -r product-research-skill/skills/product-research ~/.claude/skills/
cp -r product-research-skill/skills/product-research-service ~/.claude/skills/
cp -r product-research-skill/skills/product-research-synthesis ~/.claude/skills/
```

Restart Claude Code. The `/product-research` command will be available immediately.

> Requires Claude Code with Notion MCP configured (`mcp__notion__*` or `mcp__claude_ai_Notion__*`).

## Usage

```
/product-research AI interview tools https://www.notion.so/your-page-id
/product-research note-taking apps for developers https://www.notion.so/your-page-id
/product-research B2B onboarding automation https://www.notion.so/your-page-id
```

The Notion URL points to the **parent page** where the new research page will be created as a sub-page. If omitted, Claude will ask for it.

> [!WARNING]
> **토큰 사용량 주의 — 서비스 수를 제한하세요**
>
> 서비스 1개 분석에 약 **15,000–25,000 토큰**이 소모됩니다 (WebFetch × 3–4회 + 이미지 최대 6장 시각 해석 + Notion 쓰기 포함).
>
> | 서비스 수 | 예상 토큰 | 권장 여부 |
> |-----------|-----------|-----------|
> | 3–5개 | ~60,000–100,000 | ✅ 빠르고 가벼움 |
> | 6–8개 | ~100,000–160,000 | ✅ 균형 잡힌 리서치 |
> | 9–10개 | ~160,000–200,000 | ⚠️ 긴 세션, 컨텍스트 압축 발생 가능 |
> | 10개 초과 | ~200,000+ | ❌ 비추천 — 여러 세션으로 나눠서 진행 |
>
> **팁:** 서비스가 많으면 핵심 5–6개만 먼저 분석하고, 나중에 개별적으로 추가하세요:
> ```
> /product-research-service Notion https://www.notion.so/existing-research-page-id
> ```

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
