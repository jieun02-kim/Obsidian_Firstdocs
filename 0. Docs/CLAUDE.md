---
doc_type: policy
title: "Obsidian Vault 운영 가이드라인"
created: 2026-08-06
updated: 2026-08-06
author: "Hulkeinstein"
tags: [docs/policy, system/meta]
---

# Obsidian Vault 운영 가이드라인

## 1. 개요 및 운영 철학
본 Vault는 **Zettelkasten(지식 발전소)**과 **PARA 시스템(작업대)**을 결합하여 운영된다.
- **5. Zettelkasten/**: 시간 독립적 영구 지식 보관 (아이디어, 연구, 학습)
- **1. Projects / 2. Areas**: 시간 제약적 실행 작업 관리 (프로젝트, 목표)

---

## 2. 핵심 원칙
1. **참조 우선 원칙**: 결과물 제작 시 복사를 금지하며, 반드시 `[[링크]]` 또는 `![[임베드]]`로 원본을 참조한다.
2. **One Idea per Permanent Note**: 퍼머넌트 노트는 단 하나의 개념/주장만 담으며 명사구 또는 문장형 제목을 사용한다.
3. **연결 강제 (2+ Link Rule)**: 새로운 퍼머넌트 노트는 기존 노트 최소 2개 이상과 양방향 링크를 형성해야 한다.
4. **원천과 해석의 분리**: Literature Note(원저자 생각)와 Permanent Note(내 통찰)를 엄격히 분리한다.

---

## 3. 폴더 구조 및 규칙
- `0. Docs/`: 시스템 운영 문서 (하위 폴더 없는 평면 구조 유지)
- `1. Projects/`: 기한과 목표가 명확한 작업
- `2. Areas/`: 지속적으로 관리하는 책임 영역
- `3. Resources/`: 참고용 자료 및 관심사
- `4. Archive/`: 완료 및 중단된 프로젝트/영역 보관
- `5. Zettelkasten/`
  - `00. Inbox/`: 수집함 (주 1회 비우기)
  - `10. Literature/`: 원천 자료 요약
  - `20. Permanent/`: 정제된 내 언어의 지식

---

## 4. 메타데이터 (YAML Frontmatter) 표준
모든 마크다운 문서는 상단에 아래 표전 메타데이터 스키마를 준수한다.

```yaml
---
type: project | area | resource | literature | permanent | daily
status: active | archived | completed | in-progress | todo
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
---