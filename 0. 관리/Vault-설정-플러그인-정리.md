---
type: resource
doc_type: reference
status: active
created: 2026-08-06
updated: 2026-08-06
tags: [obsidian, 설정, 플러그인]
---

# Vault 설정 & 플러그인 정리

이 노트는 `.obsidian/` 설정 파일 기준으로 현재 vault의 플러그인 구성과 주요 설정을 정리한 참고 문서입니다. 플러그인을 추가/제거하거나 설정을 변경하면 이 노트도 함께 업데이트합니다.

## 커뮤니티 플러그인

| 플러그인 | ID | 버전 | 제작자 | 용도 |
|---|---|---|---|---|
| Git | `obsidian-git` | 2.38.6 | Vinzent | Git 백업/자동 pull·push |
| Dataview | `dataview` | 0.5.68 | Michael Brenan | 메타데이터 기반 쿼리/대시보드 |
| Templater | `templater-obsidian` | 2.24.3 | SilentVoid13 | 동적 템플릿, 스크립트 실행 |
| Kanban | `obsidian-kanban` | 2.0.51 | mgmeyers | 마크다운 기반 칸반 보드 |
| Calendar | `calendar` | 1.5.10 | Liam Cain | 데일리 노트 캘린더 뷰 |
| Terminal | `terminal` | 3.27.1 | polyipseity | Obsidian 내부 터미널 |

### Git 플러그인 설정 (`plugins/obsidian-git/data.json`)
- `autoPullOnBoot: true` — vault를 열 때 원격 저장소(origin)에서 자동으로 pull
- `autoBackupAfterFileChange: true` + `autoSaveInterval: 5` — 파일을 저장(수정/삭제/이름변경)하면 **5분 디바운스** 후 자동으로 commit + push (5분 안에 추가 수정이 있으면 타이머가 다시 5분 뒤로 밀림)
- `disablePush`, `pullBeforePush` 등은 기본값 유지 (push 활성화, push 전 pull로 충돌 방지)
- 단축키 `Ctrl/Cmd + Alt + S` → `Git: Commit-and-sync` 명령을 즉시 실행 (닫기 전 확실하게 백업하고 싶을 때 수동 실행). 등록 위치: `.obsidian/hotkeys.json`
- 참고: 이 플러그인엔 "Obsidian 종료 직전 자동 커밋" 훅은 없음 → 위 단축키로 수동 백업하거나, 5분 디바운스가 끝날 때까지 기다린 뒤 종료 권장

## 활성화된 코어 플러그인

file-explorer, global-search, switcher, graph, backlink, canvas, outgoing-link, tag-pane, properties, page-preview, daily-notes, templates, note-composer, command-palette, editor-status, bookmarks, outline, word-count, file-recovery, sync, bases

### 비활성화된 코어 플러그인
footnotes, slash-command, markdown-importer, zk-prefixer, random-note, slides, audio-recorder, workspaces, publish, webviewer

## 기타 주요 설정

| 항목 | 값 | 파일 |
|---|---|---|
| 첨부파일 저장 경로 | `7. Attachments` | `app.json` |
| 테마/외형 | 기본값 (커스텀 CSS 없음) | `appearance.json` |
| 그래프 뷰 검색 필터 | `-file:CLAUDE` (CLAUDE.md 숨김) | `graph.json` |
| 그래프 뷰 | 태그/첨부파일 노드 숨김, 고아 노트(orphan) 표시 | `graph.json` |

## 변경 이력 (Changelog)

- 2026-08-06: 노트 최초 작성. `obsidian-git` 플러그인 설치 및 `autoPullOnBoot` 활성화.
- 2026-08-06: 저장 시 자동 commit+push(`autoBackupAfterFileChange`, 5분 디바운스) 활성화, 수동 백업용 단축키(`Ctrl/Cmd+Alt+S`) 등록.
