# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

이 저장소는 **Obsidian vault**입니다. Obsidian은 마크다운 기반의 개인 지식 관리(PKM) 도구로, 로컬 파일 시스템에 마크다운 파일을 저장합니다.

## 운영 철학

복잡한 방법론(PARA, Zettelkasten 등)을 미리 갖추기보다, **실제로 쓰는 만큼만 단순하게** 유지합니다.

### 핵심 원칙

1. **네 파트 + 관리 하나**
   - `1. 개인 공부/`: 프로젝트에 종속되지 않는 개인 학습
   - `2. 논문·프로젝트/`: 논문 작업, 실행 중인 프로젝트
   - `3. Seminar/`: 연구실 세미나에서 리뷰하는 논문 정리
   - `4. 일상/`: 일상 기록
   - `0. 관리/`: 위 네 파트를 가로지르는 todo·현황 대시보드(`Dashboard.md`, 집계 전용) + Area 메모·1/2/3 인덱스 노트

2. **참조 우선 원칙**
   - 결과물 제작 시 **복사 금지**
   - 항상 `[[링크]]` / `![[임베드]]`로 참조
   - 원본은 단일 진실 공급원(Single Source of Truth)

3. **미리 만들지 않기**
   - 폴더/템플릿/구조는 실제로 반복되는 필요가 생겼을 때만 추가
   - 아직 쓸 일이 없는 하위 구조를 미리 세팅하지 않음

## 저장소 구조

```
Hulkeinstein/
├── .obsidian/              # Obsidian 설정 및 플러그인
│   ├── plugins/           # 커뮤니티 플러그인
│   │   ├── dataview/     # Dataview 플러그인 (데이터 쿼리)
│   │   ├── templater-obsidian/  # Templater 플러그인 (템플릿)
│   │   └── terminal/     # Terminal 플러그인
│   ├── core-plugins.json  # 활성화된 코어 플러그인 목록
│   ├── community-plugins.json  # 활성화된 커뮤니티 플러그인 목록
│   ├── graph.json        # 그래프 뷰 설정
│   └── workspace.json    # 워크스페이스 레이아웃
├── 0. 관리/                # 전체 todo·현황 대시보드 (콘텐츠 없음, 집계만)
├── 1. 개인 공부/            # 주제별 개인 학습 노트
├── 2. 논문·프로젝트/         # 논문/프로젝트 단위 폴더 (각각 refs/, 진행 요약/ 포함)
├── 3. Seminar/             # 연구실 세미나 리뷰 논문 정리 (논문 1편당 [번호. 논문명]/ 폴더)
├── 4. 일상/                # 일상 기록
├── 6. Templates/           # 템플릿 파일 (반복 패턴 생겼을 때만 추가)
├── 7. Attachments/         # 이미지, PDF 등 첨부 파일
└── CLAUDE.md               # Claude Code 운영 가이드
```

### 폴더별 역할

- **0. 관리**: `Dashboard.md`가 Dataview로 전체 todo·최근 활동·프로젝트 현황을 자동 수집(집계 전용, 콘텐츠 없음). 그 외에 PARA Area 메모(`사람·기관.md`, `장기 목표.md`, `워크로드.md`, `Todo.md`)와, 1/2/3 각 파트를 요약해 보여주는 인덱스 노트(`1. 개인 공부.md`, `2. 논문·프로젝트.md`, `3. Seminar.md`)를 둠. 상세 규칙: [[0. 관리/CLAUDE]]
- **1. 개인 공부**: 프로젝트에 안 묶인 개인 학습. 주제별 하위 폴더는 필요할 때마다 생성. 상세 규칙: [[1. 개인 공부/CLAUDE]]
- **2. 논문·프로젝트**: 논문/프로젝트마다 폴더 하나. 각 폴더는 `00. 개요.md`(목표/상태/todo), `refs/`(논문 레퍼런스 정리), `진행 요약/`(다른 디렉터리에서 진행 중인 실제 작업을 요청 시 스냅샷 요약)로 구성. 상세 규칙: [[2. 논문·프로젝트/CLAUDE]]
- **3. Seminar**: 연구실 세미나에서 리뷰하는 논문 정리. 논문 1편당 `[번호. 논문명]/` 폴더 하나, 그 안에 폴더와 동일한 이름의 메인 리뷰 노트 + 부가 노트. 상세 규칙: [[3. Seminar/CLAUDE]]
- **4. 일상**: 일상 기록, 데일리 노트. 상세 규칙: [[4. 일상/CLAUDE]]
- **6. Templates**: 같은 형식의 노트를 반복해서 쓰게 됐을 때만 템플릿으로 추출. 상세 규칙: [[6. Templates/CLAUDE]]
- **7. Attachments**: 이미지, PDF 등 바이너리 파일 (Git LFS 권장)

## 설치된 플러그인

### 활성화된 코어 플러그인
- **File explorer**: 파일 탐색기
- **Search**: 전역 검색
- **Graph view**: 노트 간 연결 그래프
- **Backlinks**: 역링크 표시
- **Daily notes**: 일일 노트 생성
- **Templates**: 템플릿 기능
- **Canvas**: 캔버스 보드
- **Outline**: 문서 아웃라인

### 커뮤니티 플러그인
- **Templater** (v2.16.0): 고급 템플릿 시스템
  - 동적 템플릿, 스크립트 실행, 사용자 함수 지원
- **Dataview**: 노트를 데이터베이스처럼 쿼리
  - 메타데이터 기반 검색 및 테이블 생성
- **Terminal**: Obsidian 내부 터미널
  - cmd.exe로 설정됨 (Windows)

## 작업 가이드

### 마크다운 파일 생성
- 파일명은 의미 있는 제목 사용
- 한글 파일명 지원
- 공백 대신 하이픈(-) 또는 공백 그대로 사용 가능

### Obsidian 링크 문법
```markdown
[[노트 이름]]                  # 내부 링크
[[노트 이름|표시 텍스트]]      # 별칭이 있는 링크
[[노트 이름#제목]]             # 특정 제목으로 링크
![[이미지.png]]                # 이미지 임베드
```

### Dataview 쿼리 예시

#### 1. 기본 - 모든 마크다운 파일 나열
```dataview
LIST
WHERE file.name != "CLAUDE"
SORT file.name ASC
```

#### 2. 특정 폴더의 파일 보기
```dataview
LIST
FROM "2. 논문·프로젝트"
SORT file.name ASC
```

#### 3. 태그로 필터링
```dataview
LIST
WHERE contains(tags, "project")
SORT file.name ASC
```

#### 4. TABLE 형식으로 메타데이터 표시
```dataview
TABLE type, status, created
WHERE type
SORT created DESC
```

#### 5. 전체 todo 모아보기 (0. 관리/Dashboard.md에서 사용)
```dataview
TASK
FROM "1. 개인 공부" OR "2. 논문·프로젝트" OR "3. Seminar" OR "4. 일상"
WHERE !completed
GROUP BY file.link
```

### Templater 사용
- 템플릿 폴더 설정 필요
- `<% tp.date.now() %>` 등 동적 값 삽입 가능
- JavaScript 코드 실행 가능

## 주의사항

### .obsidian 폴더
- `.obsidian/` 폴더는 이 vault의 설정을 포함하며, **다른 PC에서 동일한 환경을 재현하기 위한 단일 진실 공급원**으로 관리합니다. 저장소를 clone/pull하면 아래 설정이 그대로 적용됩니다.
- Git 추적 여부:
  - 추적함: `app.json`, `appearance.json`, `core-plugins.json`, `community-plugins.json`, `hotkeys.json`, `graph.json`, `templates.json`, `plugins/*/`(소스코드 + `data.json` 실제 설정값)
  - 제외함(`.gitignore`): `workspace.json`(개인 워크스페이스 레이아웃), `app-*.json`, `cache`
- 새 PC에서 세팅하는 법: 저장소 clone → Obsidian에서 vault로 열기 → 커뮤니티 플러그인이 이미 `plugins/`에 있으므로 "커뮤니티 플러그인 사용" 활성화만 하면 설치된 플러그인·핫키·플러그인별 설정(`data.json`)까지 동일하게 적용됨
- 플러그인 `data.json`을 새로 추가/변경할 때는 API 키나 토큰 같은 민감정보가 들어가지 않는지 커밋 전에 확인할 것

### 파일 작업
- 마크다운 파일만 생성/수정
- 이진 파일(이미지 등)은 첨부 파일 폴더에 보관 권장
- Obsidian의 내부 링크는 파일 이동 시 자동 업데이트됨

### 메타데이터 (YAML Frontmatter)
```yaml
---
tags: [태그1, 태그2]
created: 2025-10-13
author: 이름
---
```
- Dataview 쿼리에서 활용 가능
- Obsidian 속성 패널에서 시각적 편집 가능

## 보안 및 백업

### 버전 관리
- **Git 사용 권장**: 일일 커밋으로 변경 이력 추적
- **Obsidian Git 플러그인**: 자동 커밋/푸시 설정 가능 (현재 이 vault는 자동 백업 커밋이 주기적으로 실행됨 - 커밋 메시지 `vault backup: <timestamp>`)
- **커밋 메시지**: 의미 있는 메시지 작성

### 민감 정보 보호
- **디스크 암호화**: Windows BitLocker, macOS FileVault 활성화
- **공개 저장소 금지**: 개인 노트는 private repository 사용
- **민감 노트 분리**: 비공개가 필요한 내용은 별도 vault 관리

### 대용량 파일 관리
- **첨부 파일 분리**: `7. Attachments/` 폴더에 집중
- **Git LFS**: 대용량 이미지/PDF는 Git LFS 사용 고려
- **정기 정리**: 사용하지 않는 첨부 파일 주기적 삭제

### 백업 전략
```
1차: Git remote (GitHub/GitLab)
2차: 클라우드 동기화 (OneDrive/Dropbox)
3차: 외장 하드 (월 1회)
```

## 공통 속성 스키마

모든 노트에 일관된 메타데이터를 사용하여 Dataview 대시보드를 자동화합니다.

### 필수 속성 (논문·프로젝트, refs 노트에 한해)
```yaml
---
type: project | literature
status: active | in-progress | completed
created: 2025-10-13
updated: 2025-10-13
tags: []
---
```
개인 공부 / 일상 노트는 필수 스키마를 강제하지 않습니다. 열람 위주 폴더이므로 자유롭게 씁니다.

### 선택적 속성
```yaml
---
project: "[[프로젝트명]]"    # refs 노트가 속한 프로젝트
source: "[[출처]]"          # 원천 자료 (refs 노트)
author: "저자명"            # 원저자
related: ["[[노트1]]", "[[노트2]]"]  # 관련 노트
---
```

### Dataview 쿼리 실전 예시

#### 진행 중인 프로젝트 보기
```dataview
TABLE status, updated
FROM "2. 논문·프로젝트"
WHERE type = "project" AND status = "in-progress"
SORT updated DESC
```

#### refs 노트를 저자별로 그룹화
```dataview
TABLE author, source
FROM "2. 논문·프로젝트"
WHERE type = "literature"
SORT author ASC
```

## 베스트 프랙티스

1. **참조 우선**: 복사 대신 `[[링크]]`, `![[임베드]]` 사용
2. **필요할 때만 구조화**: 폴더/태그/템플릿은 실제 반복 필요가 생긴 뒤에 추가
3. **refs와 진행 요약 구분**: 외부 논문 정리(`refs/`)와 내 작업물 스냅샷(`진행 요약/`)을 섞지 않음
4. **관리 폴더는 집계 전용**: `0. 관리/`에 콘텐츠를 직접 쓰지 않고 Dashboard가 각 폴더를 가리키도록 유지
