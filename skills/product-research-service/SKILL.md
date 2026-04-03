---
name: product-research-service
description: "Use when analyzing a single product/service as part of a product research benchmark — fetches official docs and website, structures findings per a standard template, and writes the section to an existing Notion research page. Called by the product-research skill for each service in the benchmark."
argument-hint: "[service name] [notion-page-id]"
allowed-tools: WebSearch, WebFetch, mcp__notion__*, mcp__claude_ai_Notion__*
---

# Product Research — Single Service Analysis

## Purpose

Deeply analyze one product/service and write the findings to the Notion benchmark page.

## Instructions

Parse `$ARGUMENTS` as: `{service_name} {notion_page_id}`

### Step 1: Research

1. `WebSearch` for "{service_name} features pricing documentation 2024 2025"
2. `WebFetch` the official website homepage
   - Collect all image URLs found on the page (screenshots, feature images, hero images)
3. `WebFetch` the official docs / help center (if discoverable)
   - Collect additional image URLs from docs pages
4. `WebSearch` for "{service_name} changelog OR release notes OR what's new" — try to find an update log URL, then `WebFetch` it if found (skip if not found within 1 attempt)
5. `WebSearch` for "{service_name} review G2 OR Capterra" — collect 3–5 user quotes

### Step 1b: Visual Interpretation

For each collected image URL (up to 6 images — prioritize feature screenshots over logos/icons):
- `WebFetch` the image URL directly so Claude can view it
- Visually interpret what the image shows: UI layout, key elements, interaction patterns, what feature it demonstrates
- Note: which feature section this image belongs to

Use these visual observations to enrich feature descriptions. Example:
> "스크린샷에서 인터뷰 진행 중 실시간 전사 UI 확인. 좌측 질문 가이드 패널, 우측 실시간 트랜스크립트, 하단 AI 요약 바 구조"

Focus on:
- Core feature set (especially unique or AI-powered features)
- UX and interaction patterns visible in screenshots
- Pricing model and tiers
- Target customer (enterprise / SMB / individual)
- Integration ecosystem
- Recent product updates or notable launches (from update log if found)

### Step 2: Structure Findings

Build the service section following this template:

```markdown
## {Service Name}

> {One-sentence positioning: what it does, for whom, key differentiator}

### Overview
- **카테고리**: {e.g. AI 인터뷰 자동화, 사용자 조사, 데이터 분석}
- **타겟 고객**: {e.g. UX 리서처, 프로덕트 팀, 마케터}
- **가격**: {e.g. Free tier + $XX/mo Pro, 엔터프라이즈 문의}
- **웹사이트**: {url}

### 핵심 기능

<toggle: {Feature 1 Name}>
{Description — what it does, why it matters, how it works}
{Visual interpretation if screenshot was found: UI 구조, 주요 요소, 인터랙션 패턴 등}
[이미지: {image_url if found, otherwise omit}]
</toggle>

<toggle: {Feature 2 Name}>
...
</toggle>

(3–6 features total)

### UX 특징
- {UX observation 1}
- {UX observation 2}
- {UX observation 3}

### 사용자 리뷰 요약

<toggle: G2 / Capterra 리뷰>
**긍정적 피드백:**
- "{quote or paraphrase}" — {source}

**부정적 피드백 / 개선 요청:**
- "{quote or paraphrase}" — {source}
</toggle>

### 최근 업데이트
> {Latest notable release or feature update, with approximate date — skip section if no update log was found}

### vs 경쟁사
> {1–2 sentences: how this service is uniquely positioned vs others in the benchmark}
```

### Step 3: Write to Notion

Use `mcp__notion__notion-update-page` (or `mcp__claude_ai_Notion__notion-update-page`) with `update_content` command to append the service section under `## 개별 툴 분석` in the Notion page (`notion_page_id`).

### Step 4: Report

Output: "✅ {Service Name} 분석 완료"

Include a 2–3 bullet summary of the most notable findings for this service.

## Quality Standards

- Always fetch the official website — do not rely on search snippets alone
- Always attempt to fetch and visually interpret screenshots — text descriptions alone are insufficient
- Include at least 3 core features with meaningful descriptions
- User review section must have at least 1 positive and 1 critical point
- Pricing must be specific (not just "contact sales") unless truly unavailable
- The "vs 경쟁사" callout should reference at least one other service in the benchmark by name
