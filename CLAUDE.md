# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 이 저장소는 코드베이스가 아닙니다

이 디렉터리는 소프트웨어 프로젝트가 아니라 **Obsidian 볼트(노트 저장소)**입니다. 빌드, 린트, 테스트 명령어가 존재하지 않으며, 소스 코드도 없습니다.

## 운영 철학: PARA와 Zettelkasten의 분리

이 볼트는 "지금 하고 있는 일"을 위한 **PARA(작업대)**와 시간이 지나도 남는 지식을 쌓는 **Zettelkasten(지식 발전소)**을 의도적으로 분리해서 운영합니다. 두 체계를 섞지 않는 것이 핵심 원칙입니다. 각 폴더의 상세한 목적, 어떤 노트가 들어가는지, 작업 규칙은 해당 폴더의 `CLAUDE.md`를 참고하세요.

## 폴더 구조

- `0. Docs/` — Claude Code로 이 볼트를 사용할 때 필요한 참고 문서
- `1. Projects/` — 마감일이 있는 프로젝트 (PARA)
- `2. Areas/` — 지속적으로 관리하는 책임 영역 (PARA)
- `3. Resources/` — 주제별 참고 자료 (PARA)
- `4. Archive/` — 완료/비활성화된 항목 보관 (PARA)
- `5. Zettelkasten/` — 지식 발전소
  - `00. Inbox/` — 빠른 메모, 미가공 캡처
  - `10. Literature/` — 외부 원천 요약 노트
  - `20. Permanent/` — 영구 지식 노트 (원자적, 자신의 언어로)
- `6. Templates/` — Templater와 함께 쓰는 노트 템플릿
- `7. Attachments/` — 이미지, PDF 등 첨부 파일
- `.obsidian/` — Obsidian 설정 및 플러그인 디렉터리

노트 흐름의 기본 방향은 `5. Zettelkasten/00. Inbox/` → `10. Literature/` → `20. Permanent/`이며, PARA 작업 중 얻은 통찰은 Zettelkasten으로 승격시켜 지식화합니다. 완료된 PARA 항목은 `4. Archive/`로 이동하지만, Zettelkasten의 노트는 Archive로 보내지 않습니다.

## 설치된 커뮤니티 플러그인

- **Terminal** — 볼트 내에서 터미널 실행
- **Kanban** — 칸반 보드 노트
- **Calendar** — 캘린더 뷰 (데일리 노트 연동)
- **Dataview** — 노트 메타데이터/속성 기반 쿼리 및 동적 목록 생성
- **Templater** — 템플릿 기반 노트 생성

## 활성화된 핵심 기능

Daily notes, Templates, Canvas, Backlinks, Bases, Sync, Bookmarks, File recovery 등이 `.obsidian/core-plugins.json`에서 활성화되어 있습니다.

## 작업 시 유의사항

- 새 노트를 어느 폴더에 둘지 애매하면, 먼저 "마감일이 있는가(PARA)" vs "시간이 지나도 남을 지식인가(Zettelkasten)"를 기준으로 판단하세요.
- 노트 내용을 수정할 때는 Markdown 형식과 `[[위키링크]]` 문법을 유지하세요.
- `.obsidian/` 하위 설정 파일(JSON)은 Obsidian 앱이 직접 관리하는 파일이므로, 사용자가 명시적으로 요청하지 않는 한 수정하지 마세요.
