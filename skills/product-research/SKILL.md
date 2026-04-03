---
name: product-research
description: "Use when the user wants to research and benchmark multiple products/services on a topic. Creates a structured Notion page with per-service deep dives, common feature patterns with frequency rankings, and strategic implications. Invoke with a research topic (e.g. 'AI interview tools', 'note-taking apps')."
argument-hint: "[research topic] [notion-parent-page-url]"
allowed-tools: WebSearch, WebFetch, mcp__notion__*, mcp__claude_ai_Notion__*
---

# Product Research — Benchmark

## Purpose

Run an end-to-end product benchmark research session for **$ARGUMENTS**. Discover the competitive landscape, analyze each service in depth, and synthesize common patterns and strategic implications — all documented in a structured Notion page.

## Instructions

You are a senior product researcher conducting a comprehensive benchmark study.

### Step 1: Clarify Scope

Parse `$ARGUMENTS` as: `{topic} {notion-parent-page-url}`

If topic is missing, ask:
> "어떤 주제로 리서치할까요? (예: AI 인터뷰 툴, 노트 앱, 설문 자동화 서비스)"

If Notion parent page URL is missing, ask:
> "리서치 페이지를 만들 노션 페이지 URL을 알려주세요."

Always ask for research purpose (1–2 sentences):
> "이 리서치의 목적을 간단히 알려주세요. (예: '우리 제품에 벤치마킹할 분석 기능 탐색', '도입 검토를 위한 툴 비교')"

Extract the Notion page ID from the URL (the 32-char hex string in the path).

Once topic, parent page, and purpose are clear:
1. Use `WebSearch` to identify 6–10 relevant products/services for the topic.
2. Present the list to the user and confirm (add/remove services) before proceeding.

### Step 2: Create Notion Page

Create a new Notion page **under the provided parent page** using `mcp__notion__notion-create-pages` (or `mcp__claude_ai_Notion__notion-create-pages`), with `parent_id` set to the extracted page ID:

```
## 용어 정리
| 용어 | 정의 |
|------|------|
(리서치 중 등장하는 도메인 용어를 여기에 정리)

## 리서치 목적
{사용자가 입력한 리서치 목적 그대로 기재}

## 레퍼런스 리스트
| SaaS | {목적 기반 컬럼 1} | {목적 기반 컬럼 2} | {목적 기반 컬럼 3} | 적합도 | 주요 고객사 |
|------|-------------------|-------------------|-------------------|--------|------------|
(종합 단계에서 채워짐 — 컬럼은 리서치 목적에 맞게 synthesis 단계에서 확정)

## 공통 기능 패턴
| 기능 패턴 | 카테고리 | 빈도 | 설명 | 주요 레퍼런스 |
|-----------|----------|------|------|---------------|
(종합 단계에서 채워짐)

## 공백(Gap) 패턴 — 아직 없는 기능
| 기능 아이디어 | 근거 | 기회 |
|--------------|------|------|
(종합 단계에서 채워짐)

## 시사점 & 포지셔닝
(종합 단계에서 채워짐)

## 개별 분석
(각 서비스 섹션이 여기 추가됨)
```

Save the page ID for subsequent steps.

### Step 3: Analyze Each Service

For each confirmed service, invoke the `product-research-service` skill:
> Use product-research-service skill with: "[service name]" and the Notion page ID

Wait for each service analysis to complete before moving to the next.

### Step 4: Synthesize

After all services are analyzed, invoke the `product-research-synthesis` skill:
> Use product-research-synthesis skill with the Notion page ID

### Step 5: Completion

Report:
- Notion page link
- Number of services analyzed
- Top 3 common patterns found
- Top insight or differentiator

## Output Format

Always report progress after each service: "✅ {Service} 분석 완료 ({n}/{total})"

---

## Template Reference

### Per-Service Section Structure
```
## {Service Name}

> {One-line positioning statement}

### Overview
- **카테고리**: {category}
- **타겟 고객**: {target users}
- **가격**: {pricing}
- **웹사이트**: {url}

### 핵심 기능
<toggle: 기능 1>
  설명 + 스크린샷
</toggle>
...

### UX 특징
{2–3 bullet points}

### 사용자 리뷰 요약
<toggle: G2 / Capterra 리뷰>
  긍정: ...
  부정: ...
</toggle>

### vs 경쟁사
> {Callout: 이 서비스가 다른 서비스와 다른 핵심 포인트}
```
