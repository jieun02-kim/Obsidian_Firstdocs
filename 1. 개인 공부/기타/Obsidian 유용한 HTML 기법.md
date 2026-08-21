# Obsidian 유용한 HTML 기법

마크다운 문법만으로는 안 되는 표현을, Obsidian이 렌더링해주는 HTML 태그로 처리하는 방법 모음. 기본 문법 전체는 [[Obsidian 마크다운 문법]] 참고.

---

## 글자 색

```html
<span style="color:red">빨간 텍스트</span>
<span style="color:#3366cc">헥스 코드로 색 지정</span>
```
- `color`는 CSS 색상 이름(`red`, `blue`, `orange`...) 또는 헥스 코드(`#rrggbb`) 둘 다 가능

## 배경색 (커스텀 하이라이트)

```html
<span style="background-color:yellow">노란 배경</span>
<span style="background-color:#ffdddd">연한 빨강 배경</span>
```
- 기본 `==하이라이트==` 문법은 색이 테마 기본값(보통 노란색)으로 고정되는데, 이 방법으로 색을 자유롭게 지정 가능

## 글자 크기

```html
<span style="font-size:20px">큰 글자</span>
<span style="font-size:0.8em">작은 글자</span>
```

## 토글 (접기/펴기)

콜아웃 방식(마크다운 확장):
```
> [!note]- 제목
> 클릭 전까지 숨겨지는 내용
```

표준 HTML 방식 (콜아웃 스타일 없이 순수 접기만 필요할 때):
```html
<details>
<summary>펼치기 전 제목</summary>
펼치면 보이는 내용. 여기에 마크다운 문법도 그대로 사용 가능 — **굵게**, [[링크]] 등
</details>
```

## 위/아래 첨자

```html
H<sub>2</sub>O
X<sup>2</sup>
```
→ H<sub>2</sub>O, X<sup>2</sup>

## 텍스트 정렬 (가운데/오른쪽)

마크다운 표준엔 문단 정렬 문법이 없어서 `div`로 감싼다:
```html
<div style="text-align:center">가운데 정렬된 문단</div>
<div style="text-align:right">오른쪽 정렬된 문단</div>
```

## 키보드 키 표시

```html
<kbd>Ctrl</kbd> + <kbd>B</kbd>
```
→ <kbd>Ctrl</kbd> + <kbd>B</kbd> 처럼 키캡 모양으로 렌더링

## 표 셀 병합 (rowspan / colspan)

마크다운 표 문법은 셀 병합을 지원하지 않아서, 병합이 꼭 필요하면 표 전체를 HTML로 작성해야 한다:
```html
<table>
  <tr><th colspan="2">병합된 헤더</th></tr>
  <tr><td rowspan="2">세로 병합</td><td>내용1</td></tr>
  <tr><td>내용2</td></tr>
</table>
```
- 대신 마크다운 표보다 가독성이 떨어지므로, 정말 병합이 필요한 경우가 아니면 일반 마크다운 표 + 빈 칸 반복(`""`)으로 대체하는 걸 권장 (이 vault의 다른 노트들에서 이미 쓰는 방식)

## 줄바꿈 강제

```html
첫 줄<br>
둘째 줄
```
- 마크다운은 한 줄바꿈을 무시하므로(문단으로 합쳐짐), 문단 안에서 줄만 바꾸고 싶을 때 사용

---

## 주의사항
- 위 기법들은 전부 **Obsidian 읽기 모드(Reading view)에서만 정확히 렌더링**됨 — 편집 모드(Live Preview)에서도 대부분 보이지만, 일부(표 병합 등)는 읽기 모드가 더 안정적
- HTML을 과하게 쓰면 노트가 마크다운으로서의 이식성(다른 마크다운 뷰어·GitHub 등에서 열었을 때)을 잃으므로, 정말 마크다운으로 안 되는 경우에만 사용 권장
