## 1. 개인 공부

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
  dv.header(3, folder)
  const sorted = groups[folder].slice().sort((a, b) => a.file.name.localeCompare(b.file.name))
  dv.list(sorted.map(p => p.file.link))
}
```

## 2. 논문·프로젝트

```dataviewjs
const overviews = dv.pages('"2. 논문·프로젝트"')
  .where(p => p.file.name === p.file.folder.split("/").pop())
  .sort(p => p.file.folder)

dv.list(overviews.map(p => p.file.link))
```

## 3. Paper review

```dataviewjs
const papers = dv.pages('"3. Paper review"')
  .where(p => p.file.name === p.file.folder.split("/").pop())
  .sort(p => p.file.name)

dv.list(papers.map(p => p.file.link))
```

## 전체 Todo
`4. 일상`의 todo가 목록 맨 위로 오도록 정렬된다.

```dataviewjs
const folders = ["1. 개인 공부", "2. 논문·프로젝트", "3. Paper review", "4. 일상", "0. 관리"]
const inFolder = (folder, name) => folder === name || folder.startsWith(name + "/")

const pages = dv.pages()
  .where(p => folders.some(f => inFolder(p.file.folder, f)))
  .where(p => p.file.path !== "0. 관리/00_Dashboard.md")

let groups = []
for (const p of pages) {
  const tasks = p.file.tasks.where(t => !t.completed)
  if (tasks.length > 0) groups.push({ file: p.file, tasks })
}

groups.sort((a, b) => {
  const aTop = inFolder(a.file.folder, "4. 일상") ? 0 : 1
  const bTop = inFolder(b.file.folder, "4. 일상") ? 0 : 1
  if (aTop !== bTop) return aTop - bTop
  return a.file.path.localeCompare(b.file.path)
})

for (const g of groups) {
  dv.paragraph(g.file.link)
  dv.taskList(g.tasks)
}
```

vault 전체를 가로지르는 단일 진입점. todo와 최근 활동을 여기서 모아본다.

## 논문·프로젝트 현황

```dataview
TABLE status, updated
FROM "2. 논문·프로젝트"
WHERE type = "project"
SORT updated DESC
```

## 최근 수정된 노트

```dataview
TABLE file.mtime AS "수정일"
FROM "1. 개인 공부" OR "2. 논문·프로젝트" OR "3. Paper review" OR "4. 일상"
WHERE file.name != "00_Dashboard"
SORT file.mtime DESC
LIMIT 15
```
