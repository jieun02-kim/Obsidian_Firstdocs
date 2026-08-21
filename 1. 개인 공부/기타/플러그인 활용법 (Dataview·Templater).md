# 플러그인 활용법 (Dataview · Templater)

이 vault에 설치된 커뮤니티 플러그인(Dataview, Templater, Terminal) 중 콘텐츠 표현과 직접 관련된 Dataview·Templater로 만들 수 있는 기법들. Terminal은 노트 내 표현 기법이 아니라 Obsidian 안에서 cmd.exe를 쓰는 용도라 여기선 생략.

---

## Dataview — 노트를 데이터베이스처럼 쿼리

### 기본 쿼리 (DQL, ```dataview```)

|쿼리 종류|용도|
|---|---|
|`LIST`|노트 목록 나열|
|`TABLE`|메타데이터를 표로 표시|
|`TASK`|체크박스(할 일) 모아보기|
|`CALENDAR`|날짜 필드 기준 달력 뷰|

공통 절: `FROM`(대상 폴더/태그), `WHERE`(필터 조건), `SORT`(정렬), `GROUP BY`(그룹핑), `LIMIT`(개수 제한)

```dataview
LIST
FROM "2. 논문·프로젝트"
WHERE type = "project"
SORT updated DESC
```

```dataview
TABLE status, updated
FROM "2. 논문·프로젝트"
WHERE type = "project" AND status = "in-progress"
```

```dataview
TASK
FROM "1. 개인 공부" OR "2. 논문·프로젝트"
WHERE !completed
GROUP BY file.link
```

### DataviewJS (```dataviewjs```)
- DQL로 표현하기 어려운 로직(조건부 정렬, 문자열 가공, 다단계 그룹핑)이 필요할 때 사용
- 이 vault는 `.obsidian/plugins/dataview/data.json`에서 `enableDataviewJs: true`로 켜져 있어야 동작 (설정 바꾼 뒤엔 Obsidian 리로드 필요)

핵심 API:

|함수|용도|
|---|---|
|`dv.pages(source)`|페이지(노트) 목록 가져오기. `source` 생략하면 전체|
|`dv.pages().where(fn)`|조건 필터링|
|`.sort(fn)`|정렬|
|`dv.header(level, text)`|제목 렌더링 (`dv.header(2, "제목")` → `## 제목`)|
|`dv.list(array)`|불릿 목록 렌더링. 배열 원소가 `Link`면 클릭 가능한 링크로 표시|
|`dv.table(headers, rows)`|표 렌더링|
|`dv.taskList(tasks)`|체크박스 목록 렌더링|
|`dv.paragraph(text)`|일반 문단 렌더링|
|`p.file.link`|해당 페이지로 가는 Link 객체 (표시 텍스트 = 노트 이름)|
|`dv.fileLink(path, embed, displayText)`|경로로 Link 객체 직접 생성, 표시 텍스트 커스텀 가능|
|`p.file.tasks`|그 노트 안의 모든 체크박스(Task) 배열|
|`p.file.folder`|노트가 속한 폴더 경로|

**실전 예시 — 이 vault의 `0. 관리/1. 개인 공부.md`에서 쓰는 패턴** (하위 폴더를 제목2로, 그 안 노트를 불릿으로):
```dataviewjs
const pages = dv.pages('"1. 개인 공부"')
  .where(p => p.file.name !== "CLAUDE" && p.file.folder !== "1. 개인 공부")

const groups = {}
for (const p of pages) {
  const folder = p.file.folder.split("/").pop()
  if (!groups[folder]) groups[folder] = []
  groups[folder].push(p)
}

for (const folder of Object.keys(groups).sort()) {
  dv.header(2, folder)
  const sorted = groups[folder].slice().sort((a, b) => a.file.name.localeCompare(b.file.name))
  dv.list(sorted.map(p => p.file.link))
}
```

**실전 예시 — `0. 관리/00_Dashboard.md`의 "전체 Todo"** (특정 폴더 우선순위로 정렬):
```dataviewjs
const folders = ["1. 개인 공부", "2. 논문·프로젝트", "3. Paper review", "4. 일상", "0. 관리"]
const inFolder = (folder, name) => folder === name || folder.startsWith(name + "/")

const pages = dv.pages()
  .where(p => folders.some(f => inFolder(p.file.folder, f)))

let groups = []
for (const p of pages) {
  const tasks = p.file.tasks.where(t => !t.completed)
  if (tasks.length > 0) groups.push({ file: p.file, tasks })
}

for (const g of groups) {
  dv.paragraph(g.file.link)
  dv.taskList(g.tasks)
}
```

### 대시보드 만들 때 패턴
1. 프론트매터에 `type`, `status`, `updated` 같은 공통 필드를 넣어두면 `WHERE type = "..."`로 필터링 가능
2. "인덱스 노트"(어떤 폴더의 목록을 자동으로 보여주는 노트)는 DataviewJS로 만들어야 폴더 구조 변화에 자동 대응됨 — DQL의 `LIST FROM`도 되지만 제목별 그룹핑처럼 세밀한 레이아웃은 JS가 필요
3. 폴더를 옮기거나 이름을 바꾸면 FROM 경로/폴더 필터 문자열도 같이 고쳐야 함 (자동 반영 안 됨)

---

## Templater — 동적 템플릿

- 템플릿 폴더(`6. Templates/`)에 템플릿 파일을 만들고, 새 노트 생성 시 그 템플릿을 적용
- 템플릿 안에서 `<% ... %>` 문법으로 동적 값 삽입

|문법|결과|
|---|---|
|`<% tp.date.now() %>`|오늘 날짜|
|`<% tp.date.now("YYYY-MM-DD") %>`|포맷 지정한 오늘 날짜|
|`<% tp.file.title %>`|현재 파일 제목 (파일명 기반 자동 채우기에 유용)|
|`<% tp.file.creation_date() %>`|파일 생성일|
|`<% tp.system.prompt("질문") %>`|템플릿 적용 시 사용자에게 입력받기|
|`<%* ... %>`|JavaScript 코드 블록 실행 (조건문, 반복문 등)|

예시 — 새 프로젝트 노트 템플릿:
```
---
type: project
status: in-progress
created: <% tp.date.now("YYYY-MM-DD") %>
updated: <% tp.date.now("YYYY-MM-DD") %>
tags: []
---

# <% tp.file.title %>

## 목표

## Todo
- [ ]

## 진행 메모

## 참고 자료
```

- 이 vault는 "미리 만들지 않기" 원칙상, 같은 형식의 노트를 3번 이상 반복해서 쓰게 됐을 때만 템플릿으로 추출함 ([[6. Templates/CLAUDE]] 참고). 지금은 프로젝트/리뷰 노트 골격을 Claude가 그때그때 만들어주는 방식이라 아직 Templater 템플릿 파일은 없음.
