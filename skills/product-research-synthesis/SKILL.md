---
name: product-research-synthesis
description: "Use when all individual services in a product research benchmark have been analyzed — synthesizes common feature patterns with frequency rankings, gap patterns, competitive positioning map, and strategic implications into the Notion research page."
argument-hint: "[notion-page-id]"
allowed-tools: mcp__notion__*, mcp__claude_ai_Notion__*
---

# Product Research — Synthesis

## Purpose

Read all per-service sections and synthesize cross-service insights: common patterns, gaps, and strategic implications.

## Instructions

Parse `$ARGUMENTS` as: `{notion_page_id}`

### Step 1: Read All Service Sections

Fetch the Notion page content using `mcp__notion__notion-fetch` (or `mcp__claude_ai_Notion__notion-fetch`) with the page ID.

Read and internalize all service sections under `## 개별 툴 분석`.

### Step 2: Fill Reference List Table

First, determine 3 custom columns based on the research purpose stated at the start:
- Think about what dimensions matter most for this specific purpose
- Each column should answer a key question the researcher needs to compare across services
- Examples by purpose:
  - "분석 기능 벤치마킹" → 정성 데이터 수집 방식 / AI 분석 깊이 / 결과 리포트 형태
  - "도입 툴 비교" → 온보딩 난이도 / 가격 대비 가치 / 팀 협업 지원
  - "UX 리서치 툴 탐색" → 인터뷰 진행 방식 / 자동화 수준 / 리크루팅 기능

Then fill one row per service with these fixed + dynamic columns:

| 컬럼 | 내용 |
|------|------|
| **SaaS** | 서비스 이름 |
| **{목적 기반 컬럼 1}** | 해당 차원에서의 특징 (1–2문장) |
| **{목적 기반 컬럼 2}** | 해당 차원에서의 특징 (1–2문장) |
| **{목적 기반 컬럼 3}** | 해당 차원에서의 특징 (1–2문장) |
| **적합도** | 리서치 목적 기준 적합도: 높음 / 중간 / 낮음 |
| **주요 고객사** | 공개된 고객사 또는 타겟 고객 유형 |

Replace the placeholder column headers in the Notion table with the actual column names chosen.

### Step 3: Build Common Feature Pattern Table

Identify recurring features across services. For each pattern:
- Count how many services have this feature (frequency: n/total)
- Assign a category: `Core` / `Analytics` / `Collaboration` / `UX` / `AI`
- Note which services exemplify it best (for description)
- Note all services that have it (for references)

Sort by frequency descending.

Output table:

| 기능 패턴 | 카테고리 | 빈도 | 설명 | 주요 레퍼런스 |
|-----------|----------|------|------|---------------|
| {pattern} | {cat} | {n/total} | {2–3 service description with links} | {remaining services} |

Minimum 6 patterns. Include patterns with frequency ≥ 2.

### Step 3: Build Gap Pattern Table

Identify features or capabilities that:
- Appear in only 1 service (potential differentiator)
- Are requested by users but not yet implemented (from review sections)
- Represent logical next steps not yet seen anywhere

Output table:

| 기능 아이디어 | 근거 | 기회 크기 |
|--------------|------|----------|
| {feature gap} | {why it's missing / who's asking for it} | 높음 / 중간 / 낮음 |

Minimum 3 gaps.

### Step 4: Write Competitive Positioning Map

Write a 2×2 positioning analysis (text-based):

```
[포지셔닝 맵]
x축: 가격 (저가 ←→ 고가/엔터프라이즈)
y축: AI 깊이 (기본 자동화 ←→ AI-native)

사분면별 분류:
- 저가 + AI-native: {services}
- 고가 + AI-native: {services}
- 저가 + 기본 자동화: {services}
- 고가 + 기본 자동화: {services}
```

### Step 5: Write Strategic Implications

Write 4–6 bullet points covering:
- Most saturated features (table stakes — must-have)
- Underserved user needs (based on gap table)
- Differentiation opportunities
- Emerging trends across the competitive set
- Recommended positioning for a new entrant

### Step 6: Update Notion Page

Use `mcp__notion__notion-update-page` (or `mcp__claude_ai_Notion__notion-update-page`) with `update_content` to:
1. Replace `## 레퍼런스 리스트` section with the completed reference table
2. Replace `## 공통 기능 패턴` section with the completed pattern table
3. Replace `## 공백(Gap) 패턴 — 아직 없는 기능` section with the gap table
4. Replace `## 시사점 & 포지셔닝` section with positioning map + strategic implications

### Step 7: Report

Output:
- "🎉 리서치 종합 완료"
- Top 3 most common patterns
- Top 3 gaps / opportunities
- Notion page link

## Quality Standards

- Every service analyzed must appear at least once in the pattern table
- Frequency numbers must be accurate — cross-check by counting
- Positioning map must place every service in exactly one quadrant
- Strategic implications must be actionable, not generic
- Link service names to their Notion section blocks where possible
