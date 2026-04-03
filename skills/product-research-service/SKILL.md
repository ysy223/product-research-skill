---
name: product-research-service
description: "Use when analyzing a single product/service as part of a product research benchmark — fetches official docs and website, structures findings per a standard template, and writes the section to an existing Notion research page. Called by the product-research skill for each service in the benchmark."
---

# Product Research — Single Service Analysis

## Purpose

Deeply analyze one product/service and write the findings to the Notion benchmark page.

**핵심 원칙:** WebFetch의 제1 목적은 **핵심 기능의 UI가 표현된 이미지 수집**이다. 텍스트 설명보다 이미지가 먼저다.

## Instructions

Parse `$ARGUMENTS` as: `{service_name} {notion_page_id}`

### Step 1: 이미지 중심 리서치

**목표: 각 핵심 기능마다 UI 스크린샷 1장 이상 확보**

1. `WebSearch` for "{service_name} features screenshot UI 2024 2025"
   - 이미지가 풍부한 페이지 URL 우선 수집 (공식 사이트, docs, 블로그, 소개 페이지)

2. `WebFetch` 공식 홈페이지
   - 목적: 기능별 UI 스크린샷 이미지 URL 수집
   - 히어로 이미지, 기능 소개 섹션 이미지 모두 수집

3. `WebFetch` 공식 문서 / help center (발견 가능한 경우)
   - 목적: 기능별 상세 UI 이미지 추가 수집

4. `WebSearch` for "{service_name} changelog OR release notes OR what's new"
   - 목적: 최근 업데이트된 기능의 UI 이미지 확보
   - URL 발견 시 `WebFetch` → 새 기능 스크린샷 수집 (없으면 1회 시도 후 스킵)

5. `WebSearch` for "{service_name} review G2 OR Capterra" — 사용자 인용 3–5개 수집

### Step 2: 이미지 fetch & 시각 해석

수집한 이미지 URL 중 **기능 UI 스크린샷 우선 최대 8장** fetch:
- 로고, 아이콘, 배너 제외 — 실제 제품 UI가 담긴 이미지만
- 각 이미지를 `WebFetch`로 직접 열어 시각적으로 해석:
  - 어떤 기능 화면인지
  - UI 레이아웃 구조 (패널 배치, 주요 요소)
  - 인터랙션 패턴이나 흐름
- 각 이미지를 기능별로 분류 (어떤 기능 섹션에 쓸지 결정)

### Step 3: 콘텐츠 구성

아래 구조로 서비스 섹션을 작성한다.
**각 기능은 `### 타이틀 → 이미지 → 설명` 순서로 구성한다.**

```markdown
## {Service Name}

> {한 문장 포지셔닝: 무엇을, 누구를 위해, 어떤 차별점으로}

### Overview
- **카테고리**: {e.g. AI 인터뷰 자동화, 사용자 조사, 데이터 분석}
- **타겟 고객**: {e.g. UX 리서처, 프로덕트 팀, 마케터}
- **가격**: {e.g. Free tier + $XX/mo Pro, 엔터프라이즈 문의}
- **웹사이트**: {url}

### 핵심 기능

<toggle: {기능 1 이름}>

### {기능 1 이름}
![이미지]({image_url})
{이미지에서 확인된 UI 구조 및 기능 설명 — 레이아웃, 주요 요소, 인터랙션 패턴 포함}

</toggle>

<toggle: {기능 2 이름}>

### {기능 2 이름}
![이미지]({image_url})
{설명}

</toggle>

(3–6개 기능. 이미지를 확보하지 못한 기능은 텍스트 설명만 작성)

### UX 특징
- {UX 관찰 1}
- {UX 관찰 2}
- {UX 관찰 3}

### 사용자 리뷰 요약

<toggle: G2 / Capterra 리뷰>
**긍정적 피드백:**
- "{인용 또는 요약}" — {출처}

**부정적 피드백 / 개선 요청:**
- "{인용 또는 요약}" — {출처}
</toggle>

### 최근 업데이트
### {최근 업데이트된 기능 이름}
![이미지]({image_url if found})
{업데이트 내용 및 UI 설명 — 이미지 없으면 섹션 전체 생략}

### vs 경쟁사
> {이 서비스가 벤치마크 내 다른 서비스와 다른 핵심 포인트 1–2문장}
```

### Step 4: Notion에 작성

`mcp__notion__notion-update-page` (또는 `mcp__claude_ai_Notion__notion-update-page`)의 `update_content` 명령으로 `## 개별 분석` 하위에 서비스 섹션 추가.

### Step 5: 완료 리포트

"✅ {Service Name} 분석 완료" 출력 후 주요 발견 2–3줄 요약.

## Quality Standards

- **이미지 없이 기능 설명만 쓰는 것은 불충분** — 반드시 UI 스크린샷 확보 시도
- 기능 구조는 항상 `### 타이틀 → 이미지 → 설명` 순서
- 최소 3개 기능, 기능당 이미지 1장 목표
- 사용자 리뷰는 긍정/부정 각 1개 이상
- 가격은 구체적으로 (불가능한 경우에만 "문의")
- "vs 경쟁사"는 벤치마크 내 다른 서비스 이름을 명시
