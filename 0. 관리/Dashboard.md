# Dashboard

vault 전체를 가로지르는 단일 진입점. todo와 최근 활동을 여기서 모아본다.

## 전체 Todo

```dataview
TASK
FROM "1. 개인 공부" OR "2. 논문·프로젝트" OR "3. 일상"
WHERE !completed
GROUP BY file.link
```

## 최근 수정된 노트

```dataview
TABLE file.mtime AS "수정일"
FROM "1. 개인 공부" OR "2. 논문·프로젝트" OR "3. 일상"
WHERE file.name != "Dashboard"
SORT file.mtime DESC
LIMIT 15
```

## 논문·프로젝트 현황

```dataview
TABLE status, updated
FROM "2. 논문·프로젝트"
WHERE type = "project"
SORT updated DESC
```
