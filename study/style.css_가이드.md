# style.css 스터디 가이드

> **학습 목표:** style.css의 각 섹션이 어떤 화면 요소를 담당하는지 파악하고, CSS 속성 하나하나를 읽고 설명할 수 있게 됩니다.
>
> **학습 수준:** CSS 기초 지식 보유자 대상. CSS Custom Properties, Flexbox, Grid, 미디어 쿼리 등은 별도로 설명합니다.

---

## 목차
1. [파일 전체 구조 한눈에 보기](#1-파일-전체-구조-한눈에-보기)
2. [섹션 1 — CSS 변수 (Custom Properties)](#2-섹션-1--css-변수-custom-properties)
3. [섹션 2 — 리셋 & 기본 스타일](#3-섹션-2--리셋--기본-스타일)
4. [섹션 3 — 헤더](#4-섹션-3--헤더)
5. [섹션 4 — 검색 드롭다운](#5-섹션-4--검색-드롭다운)
6. [섹션 5 — 읽기 진행 바](#6-섹션-5--읽기-진행-바)
7. [섹션 6 — 히어로 섹션](#7-섹션-6--히어로-섹션)
8. [섹션 7 — 사이트 래퍼 (2단 그리드)](#8-섹션-7--사이트-래퍼-2단-그리드)
9. [섹션 8 — 공지 바](#9-섹션-8--공지-바)
10. [섹션 9 — 포스트 카드 (목록)](#10-섹션-9--포스트-카드-목록)
11. [섹션 10-11 — 포스트 상세 & 글 내용](#11-섹션-10-11--포스트-상세--글-내용)
12. [섹션 12-14 — 태그/관리자/이전다음/연관글](#12-섹션-12-14--태그관리자이전다음연관글)
13. [섹션 15-16 — 댓글 & 목록 페이지 헤더](#13-섹션-15-16--댓글--목록-페이지-헤더)
14. [섹션 17 — 페이지네이션](#14-섹션-17--페이지네이션)
15. [섹션 18-21 — 사이드바](#15-섹션-18-21--사이드바)
16. [섹션 22 — 푸터](#16-섹션-22--푸터)
17. [섹션 23 — 애니메이션 키프레임](#17-섹션-23--애니메이션-키프레임)
18. [섹션 24-26 — 반응형 디자인 (미디어 쿼리)](#18-섹션-24-26--반응형-디자인-미디어-쿼리)
19. [섹션 27-33 — 기타 페이지 & 위젯](#19-섹션-27-33--기타-페이지--위젯)

---

## 1. 파일 전체 구조 한눈에 보기

style.css는 번호가 매겨진 33개 섹션으로 구성됩니다. 주석 `/* N. 이름 */`으로 각 섹션이 시작됩니다.

```
1.  Custom Properties   — CSS 변수 정의 (색상, 크기, 폰트)
2.  Reset + Base        — 브라우저 기본 스타일 초기화
3.  Header              — 상단 헤더
4.  Search dropdown     — 검색창 드롭다운
5.  Reading progress    — 읽기 진행 바
6.  Hero section        — 메인 배너
7.  Site wrapper        — 2단 그리드 레이아웃
8.  Notice bar          — 공지사항 배너
9.  Post card           — 게시글 카드 (목록)
10. Post detail         — 게시글 상세 헤더
11. Post content (prose)— 글 본문 스타일
12. Post footer         — 태그 & 관리자 바
13. Post navigation     — 이전/다음 글
14. Related posts       — 연관 글
15. Comments            — 댓글 영역
16. List page           — 카테고리/태그/검색 목록 헤더
17. Pagination          — 페이지 번호
18. Sidebar             — 사이드바 공통
19. Sidebar: profile    — 프로필 위젯
20. Sidebar: category   — 카테고리 위젯
21. Sidebar: TOC        — 목차 위젯
22. Footer              — 하단 푸터
23. Animations          — @keyframes 애니메이션
24. Responsive 1024px   — 태블릿 반응형
25. Responsive 768px    — 모바일 반응형 (단일 컬럼)
26. Responsive 480px    — 소형 모바일
27. Tag cloud page      — 태그 페이지
28. Protected article   — 비밀글 페이지
29. Local log page      — 위치로그 페이지
30. Guestbook page      — 방명록 페이지
31. Subscribe & admin   — 구독/관리 버튼
32. Index page tweaks   — 인덱스 페이지 전용
33. Sidebar: widgets    — 사이드바 위젯들 (최근글/댓글/방문자/태그)
```

---

## 2. 섹션 1 — CSS 변수 (Custom Properties)

### 핵심 개념: CSS Custom Properties란?

> CSS 변수라고도 부릅니다. `--변수이름: 값;`으로 선언하고, `var(--변수이름)`으로 사용합니다.
> 한 곳에서 값을 바꾸면 그 변수를 사용하는 모든 곳이 한 번에 바뀝니다.

```css
:root {
  /* 색상 */
  --color-bg:        #FBFBFD;    /* 페이지 배경색 (매우 연한 흰색) */
  --color-surface:   #FFFFFF;    /* 카드/패널 배경색 (순백색) */
  --color-text-1:    #1D1D1F;    /* 주요 텍스트 (거의 검은색) */
  --color-text-2:    #86868B;    /* 보조 텍스트 (회색) */
  --color-text-3:    #A1A1A6;    /* 약한 텍스트 (연한 회색, 날짜 등) */
  --color-accent:    #007AFF;    /* 강조색 (애플 블루) */
  --color-accent-bg: #EAF3FF;    /* 강조 배경 (연한 파란 배경) */
  --color-border:    rgba(0, 0, 0, 0.08);  /* 테두리 색 (반투명 검정) */
  --color-chip-bg:   #F2F2F7;    /* 칩/태그 배경 (연한 회색) */

  /* 그림자 */
  --shadow-card:     0 4px 20px rgba(0, 0, 0, 0.05);    /* 카드 기본 그림자 */
  --shadow-hover:    0 12px 40px rgba(0, 0, 0, 0.12);   /* 카드 호버 그림자 (더 진함) */
  --shadow-header:   0 1px 0 rgba(0, 0, 0, 0.06);       /* 헤더 하단 선 그림자 */

  /* 둥근 모서리 */
  --radius-card:  20px;   /* 카드 모서리 둥글기 */
  --radius-btn:   12px;   /* 버튼 모서리 둥글기 */
  --radius-chip:  100px;  /* 태그/칩 모서리 (완전 원형) */

  /* 폰트 */
  --font: 'Pretendard Variable', 'Pretendard', -apple-system, ...;

  /* 레이아웃 치수 */
  --header-h:   60px;    /* 헤더 높이 */
  --max-prose:  800px;   /* 글 본문 최대 너비 */
  --sidebar-w:  272px;   /* 사이드바 너비 */

  /* 애니메이션 */
  --ease:       cubic-bezier(0.4, 0, 0.2, 1);  /* 가속 곡선 (Material Design 표준) */
  --dur:        0.3s;     /* 기본 전환 시간 */
  --theme-dur:  0.4s ease; /* 테마 전환 시간 */
}
```

### `:root`란?

- CSS 선택자. `<html>` 요소를 가리킴
- 여기에 선언한 변수는 **페이지 전체 어디서나** `var(--변수이름)`으로 사용 가능

### 다크모드 변수 덮어쓰기

```css
[data-theme="dark"] {
  --color-bg:      #111111;   /* 배경색을 어두운 색으로 교체 */
  --color-surface: #1C1C1E;
  --color-text-1:  #F5F5F7;   /* 텍스트는 밝은 색으로 */
  --color-accent:  #3182F6;   /* 다크모드에서 약간 밝은 파란색 */
  /* ... */
}
```

- `[data-theme="dark"]` : `<html data-theme="dark">` 상태일 때 이 블록의 변수들로 덮어씀
- JavaScript가 `document.documentElement.dataset.theme = 'dark'`를 실행하면 즉시 적용

**변수가 없으면?** 모든 색상을 직접 입력해야 합니다. 예:
```css
/* 변수 없이 */
.site-header { background: #FBFBFD; }
[data-theme="dark"] .site-header { background: #111111; }

/* 변수 있으면 */
.site-header { background: var(--color-bg); }
/* 다크모드 자동 적용 — 별도 규칙 불필요 */
```

---

## 3. 섹션 2 — 리셋 & 기본 스타일

```css
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
```

- `*` : 모든 요소를 선택
- `*::before`, `*::after` : CSS로 생성되는 가상 요소도 포함
- `box-sizing: border-box` : `padding`과 `border`를 요소의 너비/높이 안에 포함시킴. 없으면 padding을 더한 만큼 요소가 커져 레이아웃이 틀어짐
- `margin: 0; padding: 0` : 브라우저마다 다른 기본 여백을 제거

```css
html {
  scroll-behavior: smooth;
}
```
- 페이지 내 `#id` 링크를 클릭할 때 순간 이동이 아닌 **부드럽게 스크롤**

```css
body {
  font-family: var(--font);
  font-size: 1rem;
  line-height: 1.6;
  color: var(--color-text-1);
  background: var(--color-bg);
  transition: background-color var(--theme-dur), color var(--theme-dur);
  -webkit-font-smoothing: antialiased;
}
```

- `font-family` : 폰트 우선순위 목록. 앞에서부터 차례로 시도, 없으면 다음으로
- `1rem` : 루트 폰트 크기 기준 (기본 16px). `px` 대신 `rem`을 쓰면 사용자 글꼴 설정을 존중
- `line-height: 1.6` : 줄 간격. 폰트 크기의 1.6배 (가독성 향상)
- `transition` : 값이 바뀔 때 애니메이션. 테마 전환 시 배경/글자색이 서서히 변함
- `-webkit-font-smoothing: antialiased` : macOS/iOS에서 폰트 앤티앨리어싱 적용 (더 선명하게)

```css
a { color: inherit; text-decoration: none; }
img { max-width: 100%; height: auto; display: block; }
button { background: none; border: none; cursor: pointer; font-family: inherit; }
ul, ol { list-style: none; }
```

- `color: inherit` : 링크 색상을 부모 요소 색상으로 상속 (기본 파란 링크 제거)
- `text-decoration: none` : 기본 밑줄 제거
- `max-width: 100%` : 이미지가 컨테이너 밖으로 넘치지 않도록
- `display: block` : 이미지 아래에 생기는 작은 공백 제거
- `list-style: none` : `<ul>`, `<ol>`의 기본 점(•)/숫자 제거

---

## 4. 섹션 3 — 헤더

```css
.site-header {
  position: sticky;
  top: 0;
  z-index: 100;
  height: var(--header-h);
  background: rgba(251, 251, 253, 0.82);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--color-border);
  box-shadow: var(--shadow-header);
  transition: background-color var(--theme-dur), border-color var(--theme-dur);
}
```

- `position: sticky` : 스크롤해도 화면 상단에 고정됨 (`fixed`와 달리 자신의 부모 안에서만 고정)
- `top: 0` : sticky가 고정될 위치. 화면 꼭대기에서 0px 떨어진 곳
- `z-index: 100` : 다른 요소 위에 표시. 숫자가 클수록 앞에 나옴
- `rgba(251, 251, 253, 0.82)` : RGB 색상에 투명도(alpha) 0.82 = 82% 불투명. 약간 투명한 배경
- `backdrop-filter: blur(20px)` : 헤더 뒤 배경을 흐릿하게 처리 (유리 효과). 크롬/사파리에서 지원
- `-webkit-backdrop-filter` : 사파리 구버전을 위한 접두사

```css
[data-theme="dark"] .site-header {
  background: rgba(17, 17, 17, 0.82);
}
```
- 다크모드일 때만 헤더 배경색 변경

```css
.header-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
}
```

- `max-width: 1200px; margin: 0 auto` : 최대 1200px로 제한하고 가운데 정렬 (표준 레이아웃 패턴)
- `display: flex` : Flexbox 레이아웃 활성화
- `align-items: center` : 자식 요소들을 **세로 중앙** 정렬
- `justify-content: space-between` : 자식 요소들을 **양 끝**에 배치 (블로그 제목↔내비게이션)
- `gap: 16px` : flex 자식 요소 사이 간격

```css
.icon-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  border-radius: 10px;
  color: var(--color-text-2);
  transition: color var(--dur) var(--ease), background var(--dur) var(--ease), transform 0.15s var(--ease);
}

.icon-btn:hover {
  color: var(--color-text-1);
  background: var(--color-chip-bg);
}

.icon-btn:active { transform: scale(0.92); }
```

- `display: flex; align-items/justify-content: center` : 버튼 안의 아이콘을 가운데 정렬
- `:hover` : 마우스를 올렸을 때 스타일
- `:active` : 클릭하는 순간의 스타일. `scale(0.92)` = 92% 크기로 줄어드는 클릭 피드백

```css
[data-theme="light"] .icon-moon { display: none; }
[data-theme="dark"]  .icon-sun  { display: none; }
```
- 라이트 모드에서는 달 아이콘 숨김, 다크 모드에서는 해 아이콘 숨김

---

## 5. 섹션 4 — 검색 드롭다운

```css
.search-dropdown {
  display: none;
  position: absolute;
  top: calc(100% + 8px);
  right: 0;
  width: 280px;
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: 16px;
  box-shadow: var(--shadow-hover);
  overflow: hidden;
}

.search-dropdown.is-open {
  display: block;
  animation: fadeDown 0.18s var(--ease) both;
}
```

- `display: none` : 기본적으로 숨겨져 있음
- `position: absolute` : 가장 가까운 `position: relative` 부모 기준으로 위치
- `top: calc(100% + 8px)` : 부모 높이 100% + 8px 아래에 배치 (`calc()`로 계산)
- `right: 0` : 오른쪽 정렬
- `.is-open` : JavaScript가 이 클래스를 추가하면 드롭다운이 나타남
- `animation: fadeDown` : 나타날 때 위에서 아래로 스르르 내려오는 애니메이션 (섹션 23에서 정의)

---

## 6. 섹션 5 — 읽기 진행 바

```css
.reading-progress-bar {
  position: absolute;
  bottom: 0;
  left: 0;
  height: 2px;
  width: 0;
  background: var(--color-accent);
  transition: width 0.12s linear;
}
```

- `position: absolute; bottom: 0; left: 0` : 헤더 맨 아랫줄 왼쪽부터 시작
- `width: 0` : 처음엔 보이지 않음. JavaScript가 스크롤에 따라 `width`를 `0%` ~ `100%`로 변경
- `transition: width 0.12s linear` : 너비가 바뀔 때 부드럽게 애니메이션

---

## 7. 섹션 6 — 히어로 섹션

```css
.hero-section {
  display: none;  /* 기본적으로 숨김 */
}

#tt-body-index .hero-section {
  display: block;
  position: relative;
  overflow: hidden;
  height: 360px;
}
```

- `#tt-body-index .hero-section` : `id="tt-body-index"`를 가진 요소 안의 `.hero-section`에만 적용
- 티스토리가 메인 페이지에서 `<body id="tt-body-index">`로 설정하므로, 메인 페이지에서만 히어로가 보임

```css
.hero-bg {
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, #ffffff 0%, #f0f2f5 45%, #dde1e8 100%);
  background-size: cover;
  background-position: center;
}
```

- `position: absolute; inset: 0` : 부모(`.hero-section`)를 꽉 채움. `inset: 0`은 `top:0; right:0; bottom:0; left:0`의 단축
- `linear-gradient(135deg, ...)` : 135도 방향의 그라데이션. `0%` 시작 색상, `100%` 끝 색상

```css
.hero-title {
  font-size: 2.8rem;
  font-weight: 800;
  letter-spacing: -0.04em;
  line-height: 1.2;
}
```

- `font-weight: 800` : 매우 굵은 폰트 (일반 bold는 700)
- `letter-spacing: -0.04em` : 글자 간격을 살짝 좁혀 제목 느낌 강화

---

## 8. 섹션 7 — 사이트 래퍼 (2단 그리드)

```css
.site-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  padding: 48px 24px;
  display: grid;
  grid-template-columns: 1fr var(--sidebar-w);
  gap: 48px;
  align-items: start;
}
```

### 핵심 개념: CSS Grid

> `display: grid`로 활성화되는 2차원 레이아웃 시스템. 행(row)과 열(column)을 격자처럼 배치합니다.

- `grid-template-columns: 1fr var(--sidebar-w)` : 2열 구성
  - `1fr` : 남은 공간 전체를 메인 콘텐츠가 차지
  - `var(--sidebar-w)` = `272px` : 사이드바는 고정 너비
- `align-items: start` : 각 열이 콘텐츠 높이만큼만 차지 (같은 높이로 맞추지 않음)

---

## 9. 섹션 8 — 공지 바

```css
.notice-bar {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 12px 16px;
  background: var(--color-accent-bg);
  border-radius: var(--radius-btn);
  margin-bottom: 20px;
  font-size: 0.875rem;
  color: var(--color-text-1);
  transition: background var(--dur) var(--ease);
  overflow: hidden;
}

.notice-text {
  flex: 1;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

- `padding: 12px 16px` : 상하 12px, 좌우 16px 내부 여백
- `overflow: hidden` : 내용이 넘치면 잘라냄
- `flex: 1` : 남은 공간 전체를 공지 텍스트가 차지 (너무 길면 줄임표 처리)
- `white-space: nowrap` : 텍스트를 한 줄로 강제
- `text-overflow: ellipsis` : 넘치는 텍스트를 `...`으로 표시

---

## 10. 섹션 9 — 포스트 카드 (목록)

```css
.post-card {
  position: relative;
  border-radius: var(--radius-card);
  background: var(--color-surface);
  box-shadow: var(--shadow-card);
  overflow: hidden;
  margin-bottom: 14px;
  transition:
    transform var(--dur) var(--ease),
    box-shadow var(--dur) var(--ease),
    background-color var(--theme-dur);
}

.post-card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-hover);
}
```

- `position: relative` : 자식 요소의 `position: absolute` 기준점으로 지정
- `overflow: hidden` : 카드 모서리 밖으로 이미지가 삐져나오지 않도록
- `transition` : 여러 속성에 동시에 애니메이션 적용
- `translateY(-4px)` : 호버 시 4px 위로 올라가는 리프트 효과

```css
.post-card-link::after {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: var(--radius-card);
  cursor: pointer;
}
```

- 빈 내용의 가상 요소를 카드 전체에 덮어 **카드 전체를 클릭 가능**하게 만드는 패턴
- 링크(`<a>`) 안에 버튼 등 다른 클릭 요소가 있어도 카드 영역 전체로 클릭 범위를 확장

```css
.post-card-title {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
```

- 제목을 최대 **2줄**로 제한하고 넘치면 `...`으로 처리하는 패턴
- `-webkit-` 접두사가 붙은 구형 문법이지만 현재도 크로스 브라우저에서 가장 안정적

---

## 11. 섹션 10-11 — 포스트 상세 & 글 내용

```css
.post-detail {
  background: var(--color-surface);
  border-radius: var(--radius-card);
  box-shadow: 0 2px 12px rgba(0,0,0,0.08), 0 8px 32px rgba(0,0,0,0.06);
  border: 1px solid var(--color-border);
  padding: 48px 52px;
}
```

- `box-shadow` 값을 쉼표로 구분하여 **여러 그림자를 겹쳐** 더 자연스러운 깊이감 표현

### 글 본문(prose) 스타일

```css
.post-content {
  font-size: 1.0625rem;   /* 17px */
  line-height: 1.85;
  word-break: keep-all;
  overflow-wrap: break-word;
}
```

- `word-break: keep-all` : 한국어 단어를 임의로 나누지 않고 단어 단위로 줄바꿈
- `overflow-wrap: break-word` : 영어 긴 단어가 칸을 넘치면 강제로 줄바꿈

```css
.post-content h1 { font-size: 1.75rem; }
.post-content h2 { font-size: 1.4rem; }
.post-content h3 { font-size: 1.15rem; }
.post-content h4 { font-size: 1rem; }
```
- 글 본문 안의 제목들은 크기를 단계적으로 줄여 계층 구조를 표현

```css
.post-content blockquote {
  padding: 16px 20px;
  border-left: 3px solid var(--color-accent);
  background: var(--color-chip-bg);
  border-radius: 0 12px 12px 0;
  color: var(--color-text-2);
}
```
- `border-left` 만으로 인용 블록 좌측 강조선 표현
- `border-radius: 0 12px 12px 0` : 좌측은 직각, 우측만 둥근 모양

```css
.post-content pre {
  background: var(--color-chip-bg);
  border: 1px solid var(--color-border);
  border-radius: 14px;
  padding: 20px 24px;
  overflow-x: auto;
}
```
- `overflow-x: auto` : 코드 블록이 길면 가로 스크롤 생성

```css
.post-content :not(pre) > code {
  background: var(--color-chip-bg);
  border-radius: 6px;
  padding: 2px 6px;
  color: var(--color-accent);
}
```
- `:not(pre) > code` : `<pre>` 안이 아닌(= 인라인) `<code>`만 선택
- `pre` 안의 코드블록과 인라인 코드(`코드`)를 다르게 스타일링

---

## 12. 섹션 12-14 — 태그/관리자/이전다음/연관글

```css
.post-tags a {
  display: inline-block;
  font-size: 0.78rem;
  background: var(--color-chip-bg);
  padding: 4px 12px;
  border-radius: var(--radius-chip);
  transition: background var(--dur), color var(--dur);
}

.post-tags a:hover {
  background: var(--color-accent);
  color: #fff;
}
```
- 티스토리가 `[##_tag_label_rep_##]`을 `<a>` 태그들로 교체하므로, `.post-tags a`로 태그 스타일 지정

```css
.post-nav {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
  margin-top: 36px;
}

.post-nav-next { text-align: right; }
.post-nav-next .post-nav-label { justify-content: flex-end; }
```
- 이전/다음 버튼을 Grid로 좌우 절반씩 나눔

```css
.related-posts-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 10px;
}
```
- `repeat(auto-fill, minmax(150px, 1fr))` : 컨테이너 너비에 따라 열 수가 자동으로 변하는 반응형 그리드
  - 각 열은 최소 150px, 최대 1fr (남은 공간 균등 배분)

---

## 13. 섹션 15-16 — 댓글 & 목록 페이지 헤더

```css
.comments-section {
  margin-top: 48px;
  padding-top: 36px;
  border-top: 1px solid var(--color-border);
}
```
- `border-top` : 댓글 섹션 위에 구분선 표시

```css
.list-page-badge {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  font-size: 0.72rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  color: var(--color-accent);
  background: var(--color-accent-bg);
  padding: 4px 10px;
  border-radius: var(--radius-chip);
}
```
- `text-transform: uppercase` : 영문을 모두 대문자로
- `letter-spacing: 0.06em` : 대문자 배지에서 자주 쓰는 자간 넓히기 패턴

---

## 14. 섹션 17 — 페이지네이션

```css
.page-btn,
.page-num {
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 40px;
  height: 40px;
  padding: 0 10px;
  border-radius: var(--radius-btn);
  font-size: 0.875rem;
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  transition: background var(--dur), color var(--dur), transform var(--dur);
}

/* 티스토리가 현재 페이지 버튼에 "on" 클래스를 자동으로 추가 */
.page-num.on {
  background: var(--color-accent);
  color: #fff;
  border-color: var(--color-accent);
}
```
- `.page-btn, .page-num` : 쉼표로 여러 선택자에 동일한 스타일 한 번에 적용
- `.page-num.on` : `class="page-num on"` 요소에만 적용. 현재 페이지 강조

---

## 15. 섹션 18-21 — 사이드바

### 사이드바 공통

```css
.site-sidebar {
  position: sticky;
  top: calc(var(--header-h) + 20px);
  display: flex;
  flex-direction: column;
  gap: 14px;
  max-height: calc(100vh - var(--header-h) - 40px);
  overflow-y: auto;
  scrollbar-width: none;
}

.site-sidebar::-webkit-scrollbar { display: none; }
```

- `position: sticky; top: calc(...)` : 스크롤 시 헤더 아래에 고정
- `100vh` : 화면 높이 100%. `max-height`로 사이드바가 화면을 넘지 않도록 제한
- `overflow-y: auto` : 사이드바 내용이 많으면 내부 스크롤 생성
- `scrollbar-width: none` : Firefox에서 스크롤바 숨김
- `::-webkit-scrollbar` : Chrome/Safari에서 스크롤바 숨김

```css
.sidebar-widget {
  background: var(--color-surface);
  border-radius: var(--radius-card);
  box-shadow: var(--shadow-card);
  padding: 22px;
}
```

### 카테고리 위젯 (복잡한 티스토리 HTML 대응)

```css
.sidebar-category {
  background: transparent !important;
  box-shadow: none !important;
  padding: 10px 0 !important;
}
```
- `!important` : 다른 곳에서 지정된 스타일보다 이 값을 강제 적용
- 티스토리가 카테고리 HTML을 자체 구조로 출력하므로 기본 위젯 스타일을 무력화

```css
.sidebar-category a::before {
  content: '#';
  color: var(--color-accent);
  font-weight: 700;
}

.sidebar-category a.link_sub_item::before {
  content: '·';
  color: var(--color-text-3);
}
```

- `::before` : 요소 앞에 CSS로 내용을 삽입하는 가상 요소
- 카테고리 링크 앞에 `#` 기호, 서브카테고리 앞에 `·` 기호를 자동 추가

```css
.sidebar-category .selected > a,
.sidebar-category .current_cat > a {
  color: var(--color-accent);
  font-weight: 700;
}
```

- `.selected > a` : `.selected`의 **직접 자식** `<a>`만 선택 (`>` = 직접 자식 결합자)
- 현재 보고 있는 카테고리를 강조 표시

### TOC 위젯

```css
.sidebar-toc { display: none; }  /* JavaScript가 조건에 맞으면 display: block으로 변경 */

.toc-link.is-active {
  color: var(--color-text-1);
  font-weight: 600;
  border-left-color: var(--color-accent);
  background: var(--color-accent-bg);
}
```

---

## 16. 섹션 22 — 푸터

```css
.site-footer {
  background: var(--color-surface);
  border-top: 1px solid var(--color-border);
  transition: background-color var(--theme-dur), border-color var(--theme-dur);
}

.footer-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 28px 24px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
}
```

- 헤더와 같은 `max-width + margin: 0 auto` 패턴으로 가운데 정렬

---

## 17. 섹션 23 — 애니메이션 키프레임

```css
@keyframes fadeDown {
  from { opacity: 0; transform: translateY(-6px); }
  to   { opacity: 1; transform: translateY(0); }
}
```

- `@keyframes 이름` : 애니메이션 동작을 단계별로 정의
- `from` → `to` : 시작 상태에서 끝 상태로 전환
- `opacity: 0` → `opacity: 1` : 투명에서 불투명으로 (페이드인)
- `translateY(-6px)` → `translateY(0)` : 6px 위에서 제자리로 (슬라이드 다운)

**사용하는 곳:** `.search-dropdown.is-open { animation: fadeDown 0.18s ... }`

---

## 18. 섹션 24-26 — 반응형 디자인 (미디어 쿼리)

### 핵심 개념: @media 쿼리

> 화면 크기에 따라 다른 CSS를 적용하는 문법. 모바일/태블릿/PC마다 다른 레이아웃을 구성.

### 1024px 이하 (태블릿)

```css
@media (max-width: 1024px) {
  :root { --sidebar-w: 240px; }
  .site-wrapper { gap: 32px; }
  .post-detail { padding: 36px 32px; }
}
```
- CSS 변수 `--sidebar-w`를 240px로 줄임

### 768px 이하 (모바일 — 주요 변경)

```css
@media (max-width: 768px) {
  :root { --header-h: 56px; }

  .nav-link { display: none; }          /* 상단 내비 링크 숨김 */
  .mobile-menu-btn { display: flex; }   /* 햄버거 버튼 표시 */

  .site-wrapper {
    grid-template-columns: 1fr;  /* 2열 → 1열로 변경 */
    padding: 24px 16px;
    gap: 0;
  }

  /* 사이드바: 화면 밖 패널로 전환 */
  .site-sidebar {
    position: fixed;
    top: 0;
    right: -100%;           /* 화면 오른쪽 밖으로 숨김 */
    width: min(320px, 86vw);
    height: 100dvh;
    background: var(--color-surface);
    box-shadow: -8px 0 40px rgba(0,0,0,0.18);
    z-index: 90;
    transition: right 0.28s var(--ease), background-color var(--theme-dur);
  }

  .site-sidebar.is-open { right: 0; }  /* JavaScript가 이 클래스를 추가 */
}
```

- `grid-template-columns: 1fr` : 2열 그리드를 1열로 변경 → 사이드바가 아래로 내려감
- `position: fixed; right: -100%` : 사이드바를 화면 밖에 숨겨두는 오프캔버스 패턴
- `right: 0` : 클래스가 추가되면 화면 안으로 슬라이드인
- `min(320px, 86vw)` : 320px와 화면 너비의 86% 중 **작은 값** 선택

```css
  body.sidebar-open::after {
    content: '';
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.38);
    z-index: 89;
    animation: fadeIn 0.28s var(--ease);
  }
```
- 사이드바가 열릴 때 뒤 배경을 어둡게 하는 딤 레이어
- `z-index: 89` : 사이드바(90) 뒤, 나머지 콘텐츠 앞에 배치

### 480px 이하 (소형 모바일)

```css
@media (max-width: 480px) {
  .post-card-inner {
    flex-direction: column-reverse;
    padding: 18px;
  }

  .post-card-thumb {
    width: 100%;
    height: 190px;
    align-self: stretch;
  }
}
```
- `flex-direction: column-reverse` : Flex 방향을 위아래로 바꾸고 순서를 반대로 (썸네일이 위로)
- `align-self: stretch` : 너비를 부모 전체로 늘림

---

## 19. 섹션 27-33 — 기타 페이지 & 위젯

### 태그 클라우드

```css
.tag-item.cloud1 { font-size: 1.1rem; font-weight: 700; color: var(--color-accent); }
.tag-item.cloud2 { font-size: 1.0rem; font-weight: 600; }
.tag-item.cloud3 { font-size: 0.9rem; }
.tag-item.cloud4 { font-size: 0.82rem; }
.tag-item.cloud5 { font-size: 0.78rem; color: var(--color-text-3); }
```
- 티스토리가 태그 사용 빈도에 따라 `cloud1`(가장 많이 씀) ~ `cloud5`(가장 적게 씀) 클래스를 자동 부여
- CSS에서 각 클래스별 크기를 다르게 지정해 **시각적 태그 클라우드** 구현

### 관리자 버튼

```css
.profile-admin-btns { display: none; }

.profile-admin-btns.owner,
.profile-admin-btns.member {
  display: flex !important;
}
```
- 기본은 숨김. `[##_role_group_##]`이 `owner` 또는 `member`로 교체되면 버튼이 표시

### 인덱스 페이지 전용

```css
#tt-body-index .list-page-cover { display: none; }
#tt-body-index .list-page-desc  { display: none; }
```
- 메인 페이지에서만 카테고리 커버 이미지와 설명을 숨김
