# skin.html 스터디 가이드

> **학습 목표:** 이 파일을 처음부터 끝까지 읽으며 각 코드 블록이 무슨 역할을 하는지 설명할 수 있게 됩니다.
>
> **학습 수준:** HTML 기초 지식 보유자 대상. 티스토리 고유 태그(`s_*`, `[##_..._##]`)는 별도로 설명합니다.

---

## 목차
1. [전체 파일 구조](#1-전체-파일-구조)
2. [head 영역](#2-head-영역)
3. [티스토리 핵심 개념: 치환자와 치환 태그](#3-티스토리-핵심-개념-치환자와-치환-태그)
4. [HEADER — 헤더](#4-header--헤더)
5. [HERO — 메인 배너](#5-hero--메인-배너)
6. [MAIN LAYOUT — 2단 레이아웃](#6-main-layout--2단-레이아웃)
7. [NOTICE — 공지사항](#7-notice--공지사항)
8. [LIST HEADER — 목록 페이지 헤더](#8-list-header--목록-페이지-헤더)
9. [ARTICLE — 게시글 목록 & 상세](#9-article--게시글-목록--상세)
10. [PROTECTED — 비밀글](#10-protected--비밀글)
11. [PAGE REP — 페이지 타입 글](#11-page-rep--페이지-타입-글)
12. [PAGING — 페이지네이션](#12-paging--페이지네이션)
13. [TAG / LOCAL / GUEST — 기타 페이지](#13-tag--local--guest--기타-페이지)
14. [SIDEBAR — 사이드바](#14-sidebar--사이드바)
15. [FOOTER — 푸터](#15-footer--푸터)
16. [SCRIPT — 자바스크립트](#16-script--자바스크립트)

---

## 1. 전체 파일 구조

```html
<!DOCTYPE html>
<html lang="ko" data-theme="light">
<head> ... </head>
<body id="[##_body_id_##]">
<s_t3>

  <!-- HEADER -->
  <!-- HERO -->
  <!-- MAIN LAYOUT (main + aside) -->
  <!-- FOOTER -->
  <!-- SCRIPT -->

</s_t3>
</body>
</html>
```

- `<!DOCTYPE html>` : "이 파일은 HTML5 문서입니다"라고 브라우저에 알리는 선언
- `<html lang="ko">` : 문서의 언어가 한국어임을 명시. 검색엔진과 스크린리더가 활용
- `data-theme="light"` : HTML 커스텀 속성(data attribute). CSS에서 `[data-theme="dark"]`처럼 읽어 다크/라이트 테마를 전환하는 데 사용
- `<s_t3>` : **티스토리 전용 태그.** 아래 [섹션 3](#3-티스토리-핵심-개념-치환자와-치환-태그)에서 자세히 설명

---

## 2. head 영역

```html
<head>
  <title>[##_page_title_##]</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta charset="utf-8" />
  <meta name="title" content="[##_page_title_##] :: [##_title_##]" />
  <link rel="alternate" type="application/rss+xml" title="[##_title_##]" href="[##_rss_url_##]" />
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/xeicon@2.3.3/xeicon.min.css">
  <link rel="stylesheet" href="./style.css" />
  ...
</head>
```

### 핵심 태그/속성 설명

- `<title>` : 브라우저 탭에 표시되는 제목. `[##_page_title_##]`은 티스토리가 현재 페이지 제목으로 자동 교체
- `<meta charset="utf-8">` : 한글 등 다국어 문자가 깨지지 않도록 인코딩을 UTF-8로 지정
- `<meta name="viewport" ...>` : 모바일 화면에서 화면 크기에 맞게 렌더링되도록 지시. 없으면 모바일에서 PC 화면처럼 작게 보임
- `<link rel="stylesheet" href="./style.css">` : 같은 폴더의 `style.css` 파일을 불러옴
- `<link rel="alternate" type="application/rss+xml">` : RSS 피드 주소를 브라우저/리더에 알림

### 테마 초기화 스크립트

```html
<script>
  (function () {
    var saved = localStorage.getItem('atm-theme');
    var preferred = window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';
    document.documentElement.dataset.theme = saved || preferred;
  }());
</script>
```

- CSS가 그려지기 **전에** 실행되어 화면이 깜빡이는 현상(flash)을 방지
- `localStorage.getItem('atm-theme')` : 사용자가 이전에 선택한 테마를 브라우저 저장소에서 읽음
- `window.matchMedia(...)` : OS 다크모드 설정을 감지
- `document.documentElement.dataset.theme` : `<html data-theme="...">` 값을 변경

### 커버 이미지 조건부 스타일

```html
<s_if_var_cover-image>
<style>.hero-bg { background-image: url('[##_var_cover-image_##]') !important; }</style>
</s_if_var_cover-image>
```

- `<s_if_var_cover-image>` : **티스토리 조건 태그.** 스킨 설정에서 `cover-image` 변수가 설정된 경우에만 내부 내용을 출력
- `[##_var_cover-image_##]` : 스킨 설정에서 사용자가 업로드한 이미지 URL로 교체됨

---

## 3. 티스토리 핵심 개념: 치환자와 치환 태그

티스토리 스킨에는 일반 HTML에 없는 두 가지 특수 문법이 있습니다.

### 3-1. 치환자 `[##_이름_##]`

> 티스토리 서버가 HTML을 브라우저로 보내기 전에 **실제 값으로 바꿔주는** 자리표시자

| 치환자 | 교체되는 값 |
|--------|------------|
| `[##_title_##]` | 블로그 이름 |
| `[##_blog_link_##]` | 블로그 주소 (예: `https://myblog.tistory.com/`) |
| `[##_page_title_##]` | 현재 페이지 제목 |
| `[##_body_id_##]` | 현재 페이지 유형 (예: `tt-body-index`, `tt-body-article`) |
| `[##_article_rep_title_##]` | 게시글 제목 |
| `[##_article_rep_desc_##]` | 게시글 본문 |
| `[##_article_rep_date_##]` | 게시글 날짜 |
| `[##_rss_url_##]` | RSS 피드 URL |
| `[##_count_total_##]` | 총 방문자 수 |

### 3-2. 치환 태그 `<s_이름>...</s_이름>`

> 특정 조건이 맞거나, 반복 데이터가 있을 때만 **감싼 내용을 출력**하는 티스토리 전용 태그

| 태그 | 역할 |
|------|------|
| `<s_t3>` | 스킨 전체를 감싸는 최상위 래퍼. 반드시 있어야 함 |
| `<s_index_article_rep>` | 목록 페이지(인덱스)일 때만 내부 출력 |
| `<s_permalink_article_rep>` | 상세 페이지(개별 글)일 때만 내부 출력 |
| `<s_article_rep>` | 게시글 반복 블록 (목록의 각 글마다 반복) |
| `<s_notice_rep>` | 공지사항이 있을 때 출력 |
| `<s_paging>` | 페이지가 2페이지 이상일 때 출력 |
| `<s_paging_rep>` | 각 페이지 번호마다 반복 |
| `<s_sidebar>` | 사이드바 영역 |
| `<s_sidebar_element>` | 사이드바 위젯 하나 |
| `<s_rp>` | 댓글 기능이 활성화된 경우 출력 |
| `<s_rp_count>` | 댓글 수가 있을 때 출력 |
| `<s_tag>` | 태그 페이지일 때 출력 |
| `<s_tag_label>` | 게시글에 태그가 있을 때 출력 |
| `<s_list>` | 카테고리/검색/태그 목록 페이지일 때 출력 |
| `<s_list_image>` | 카테고리에 대표 이미지가 있을 때 출력 |
| `<s_list_empty>` | 목록이 비어 있을 때 출력 |
| `<s_guest>` | 방명록 페이지일 때 출력 |
| `<s_local>` | 위치로그 페이지일 때 출력 |
| `<s_article_prev>` | 이전 글이 있을 때 출력 |
| `<s_article_next>` | 다음 글이 있을 때 출력 |
| `<s_article_related>` | 연관 글이 있을 때 출력 |
| `<s_article_protected>` | 비밀글일 때 출력 |
| `<s_page_rep>` | 페이지 타입(공지) 글일 때 출력 |
| `<s_if_var_이름>` | 스킨 변수가 설정된 경우 출력 |
| `<s_ad_div>` | 블로그 관리자(소유자)일 때만 출력 |
| `<s_rct_notice>` | 최근 공지사항이 있을 때 출력 |
| `<s_rctps_rep>` | 최근 게시글 목록 반복 |
| `<s_rctrp_rep>` | 최근 댓글 목록 반복 |
| `<s_random_tags>` | 랜덤 태그 클라우드 반복 |
| `<s_article_rep_thumbnail>` | 게시글 썸네일이 있을 때 출력 |
| `<s_article_related_rep>` | 연관 글 목록 반복 |
| `<s_article_related_rep_thumbnail>` | 연관 글 썸네일이 있을 때 출력 |
| `<s_rct_notice_rep>` | 최근 공지사항 목록 반복 |

---

## 4. HEADER — 헤더

```html
<header class="site-header" id="siteHeader">
  <div class="header-inner">
    <h1 class="site-title">
      <a href="[##_blog_link_##]">[##_title_##]</a>
    </h1>
    <nav class="site-nav" id="siteNav">
      <a href="[##_blog_link_##]" class="nav-link">홈</a>
      <a href="[##_taglog_link_##]" class="nav-link">태그</a>
      <a href="[##_guestbook_link_##]" class="nav-link">방명록</a>
      ...
    </nav>
  </div>
  <div class="reading-progress-bar" id="readingProgress" ...></div>
</header>
```

- `<header>` : 페이지 상단 헤더를 나타내는 시맨틱 태그
- `class="site-header"` : CSS에서 `.site-header { ... }`로 스타일을 적용하는 이름표
- `id="siteHeader"` : JavaScript에서 `document.getElementById('siteHeader')`로 이 요소를 찾을 때 사용
- `<h1>` : 페이지에서 가장 중요한 제목. 보통 사이트 이름에 사용
- `<nav>` : 내비게이션 링크 모음임을 나타내는 시맨틱 태그
- `[##_taglog_link_##]` : 태그 모음 페이지 URL로 교체
- `[##_guestbook_link_##]` : 방명록 페이지 URL로 교체

### 검색 드롭다운

```html
<div class="search-wrap">
  <button class="icon-btn search-toggle" id="searchToggle"
          aria-label="검색 열기" aria-expanded="false">
    <svg ...></svg>
  </button>
  <div class="search-dropdown" id="searchDropdown" role="search">
    <form class="search-form"
          onsubmit="location.href='[##_blog_link_##]/search/'+encodeURIComponent(this.q.value);return false;">
      <input type="text" name="q" class="search-input" placeholder="검색어를 입력하세요">
      <button type="submit">...</button>
    </form>
  </div>
</div>
```

- `aria-label` : 스크린리더가 읽어주는 설명. 시각 장애인 접근성을 위함
- `aria-expanded="false"` : 드롭다운이 현재 닫혀 있음을 알림 (JavaScript가 `true`로 바꿈)
- `<svg>` : 이미지 파일 없이 HTML 코드로 그린 벡터 아이콘. 확대해도 선명
- `role="search"` : 이 영역이 검색 기능임을 보조 기기에 알림
- `onsubmit="..."` : 폼 제출 시 실행되는 인라인 JavaScript. 검색어를 URL에 붙여 이동
- `encodeURIComponent(...)` : 한글 등 특수문자가 URL에서 깨지지 않도록 인코딩

### 읽기 진행 바

```html
<div class="reading-progress-bar" id="readingProgress"
     role="progressbar" aria-label="읽기 진행도"></div>
```

- 빈 `<div>`. JavaScript가 스크롤 위치에 따라 `style.width` 값을 조절하여 진행률 바를 표시

---

## 5. HERO — 메인 배너

```html
<section class="hero-section" aria-label="블로그 소개">
  <div class="hero-bg" aria-hidden="true"></div>
  <div class="hero-overlay" aria-hidden="true"></div>
  <div class="hero-content">
    <div class="hero-info">
      <h2 class="hero-title">[##_title_##]</h2>
      <p class="hero-desc">[##_desc_##]</p>
    </div>
  </div>
</section>
```

- `<section>` : 하나의 독립적인 콘텐츠 구역을 나타내는 시맨틱 태그
- `aria-hidden="true"` : 배경 이미지/오버레이는 장식용이므로 스크린리더가 읽지 않도록 숨김
- `[##_desc_##]` : 블로그 소개글로 교체
- CSS에서 `#tt-body-index .hero-section { display: block; }`으로 **인덱스 페이지에서만** 표시됨
  - `[##_body_id_##]` → `tt-body-index` (메인 페이지), `tt-body-article` (글 상세 페이지) 등으로 교체
  - 티스토리가 `<body id="tt-body-index">`처럼 설정해 CSS 선택자로 페이지 유형을 구분

---

## 6. MAIN LAYOUT — 2단 레이아웃

```html
<div class="site-wrapper">
  <main class="main-content" id="mainContent">
    <!-- 게시글 목록, 상세, 공지, 페이지네이션 등 -->
  </main>

  <aside class="site-sidebar" id="siteSidebar" aria-label="사이드바">
    <!-- 프로필, TOC, 카테고리, 최근글 등 -->
  </aside>
</div>
```

- `<main>` : 페이지의 핵심 콘텐츠 영역을 나타내는 시맨틱 태그. 페이지당 하나만 사용
- `<aside>` : 주 콘텐츠와 연관되지만 부가적인 영역 (사이드바)
- CSS `grid-template-columns: 1fr var(--sidebar-w)`로 **좌측 메인 + 우측 사이드바** 2단 구성

---

## 7. NOTICE — 공지사항

```html
<s_notice_rep>
  <s_index_article_rep>
  <a href="[##_notice_rep_link_##]" class="notice-bar">
    <span class="notice-chip">공지</span>
    <span class="notice-text">[##_notice_rep_title_##]</span>
    <svg ...></svg>
  </a>
  </s_index_article_rep>

  <s_permalink_article_rep>
  <article class="post-detail" ...>
    ...
    <h1 class="post-detail-title">[##_notice_rep_title_##]</h1>
    ...
    <div class="post-content">[##_notice_rep_desc_##]</div>
  </article>
  </s_permalink_article_rep>
</s_notice_rep>
```

- `<s_notice_rep>` : 공지사항이 존재할 때만 이 블록 전체를 출력
- `<s_index_article_rep>` : 현재 페이지가 **목록 페이지**이면 공지를 배너(링크)로 표시
- `<s_permalink_article_rep>` : 현재 페이지가 **상세 페이지**이면 공지를 전체 글로 표시
- `[##_notice_rep_title_##]` : 공지사항 제목으로 교체
- `[##_notice_rep_desc_##]` : 공지사항 본문으로 교체
- `<article>` : 독립적으로 의미 있는 콘텐츠 블록 (글, 뉴스 등)

---

## 8. LIST HEADER — 목록 페이지 헤더

```html
<s_list>
<div class="list-page-header">
  <s_list_image>
  <div class="list-page-cover" style="background-image:url('[##_list_image_##]')"></div>
  </s_list_image>
  <div class="list-page-eyebrow">
    <span class="list-page-badge">카테고리</span>
  </div>
  <h2 class="list-page-title">
    [##_list_conform_##]
    <span class="list-page-count">[##_list_count_##]건</span>
  </h2>
  <p class="list-page-desc">[##_list_description_##]</p>
  <s_list_empty>
  <div class="list-empty">등록된 글이 없습니다.</div>
  </s_list_empty>
</div>
</s_list>
```

- `<s_list>` : 카테고리/검색/태그 결과 **목록 페이지**일 때만 출력
- `style="background-image:url(...)"` : 인라인 스타일로 배경 이미지를 동적으로 지정
- `[##_list_conform_##]` : 현재 목록의 제목 (카테고리명, 검색어, 태그명 등)으로 교체
- `[##_list_count_##]` : 목록에 포함된 글 수로 교체
- `[##_list_description_##]` : 카테고리 설명으로 교체
- `<s_list_empty>` : 목록이 비어 있을 때만 "등록된 글이 없습니다" 출력

---

## 9. ARTICLE — 게시글 목록 & 상세

```html
<s_article_rep>

  <!-- 상세 페이지: 전체 글 표시 -->
  <s_permalink_article_rep>
  <article class="post-detail" itemscope itemtype="http://schema.org/BlogPosting">
    <header class="post-detail-header">
      <div class="post-detail-top-row">
        <div class="post-detail-meta">
          <a href="[##_article_rep_category_link_##]" class="post-category">
            [##_article_rep_category_##]
          </a>
          <time class="post-date" itemprop="datePublished">
            [##_article_rep_date_##]
          </time>
          <s_rp_count>
          <span class="post-comment-count">
            <svg ...></svg>
            [##_article_rep_rp_cnt_##]
          </span>
          </s_rp_count>
        </div>
        <s_ad_div>
        <div class="post-admin-bar">
          <a href="[##_s_ad_m_link_##]" class="admin-btn">수정</a>
          <a href="#" onclick="[##_s_ad_d_onclick_##]" class="admin-btn admin-btn-danger">삭제</a>
        </div>
        </s_ad_div>
      </div>
      <h1 class="post-detail-title">[##_article_rep_title_##]</h1>
    </header>

    <div class="post-content" id="postContent" itemprop="articleBody">
      [##_article_rep_desc_##]
    </div>

    <footer class="post-detail-footer">
      <s_tag_label>
      <div class="post-tags">[##_tag_label_rep_##]</div>
      </s_tag_label>
    </footer>

    <!-- 이전/다음 글 내비게이션 -->
    <!-- 연관 글 -->
    <!-- 댓글 -->
  </article>
  </s_permalink_article_rep>

  <!-- 목록 페이지: 카드 형식 -->
  <s_index_article_rep>
  <article class="post-card">
    <div class="post-card-inner">
      <div class="post-card-body">
        <h2 class="post-card-title">
          <a href="[##_article_rep_link_##]">[##_article_rep_title_##]</a>
        </h2>
        <p class="post-card-summary">[##_article_rep_summary_##]</p>
      </div>
      <s_article_rep_thumbnail>
      <div class="post-card-thumb">
        <img src="[##_article_rep_thumbnail_url_##]" alt="" loading="lazy">
      </div>
      </s_article_rep_thumbnail>
    </div>
  </article>
  </s_index_article_rep>

</s_article_rep>
```

- `<s_article_rep>` : 게시글 데이터를 반복 출력하는 최상위 래퍼
- `itemscope itemtype="http://schema.org/BlogPosting"` : 구글 검색에서 구조화 데이터로 인식하기 위한 마크업
- `itemprop="datePublished"` / `itemprop="articleBody"` : 구조화 데이터의 필드 지정
- `<time>` : 날짜/시간임을 나타내는 시맨틱 태그
- `<s_ad_div>` : 블로그 관리자에게만 수정/삭제 버튼을 보여주는 조건 태그
- `[##_article_rep_desc_##]` : 글 본문 HTML 전체로 교체
- `[##_article_rep_summary_##]` : 글의 요약문으로 교체
- `[##_tag_label_rep_##]` : 태그 링크 목록(`<a>` 태그들)으로 교체
- `loading="lazy"` : 화면에 보일 때만 이미지를 불러오는 지연 로딩 속성

### 이전/다음 글 내비게이션

```html
<nav class="post-nav" aria-label="이전/다음 글">
  <s_article_prev>
  <a href="[##_article_prev_link_##]" class="post-nav-item post-nav-prev">
    <span class="post-nav-label">이전 글</span>
    <span class="post-nav-title">[##_article_prev_title_##]</span>
  </a>
  </s_article_prev>
  <s_article_next>
  <a href="[##_article_next_link_##]" class="post-nav-item post-nav-next">
    <span class="post-nav-label">다음 글</span>
    <span class="post-nav-title">[##_article_next_title_##]</span>
  </a>
  </s_article_next>
</nav>
```

- `<s_article_prev>` / `<s_article_next>` : 이전/다음 글이 있을 때만 해당 링크 출력

### 연관 글

```html
<s_article_related>
<section class="related-posts">
  <h2>같은 카테고리 글</h2>
  <div class="related-posts-grid">
    <s_article_related_rep>
    <a href="[##_article_related_rep_link_##]" class="related-post-card [##_article_related_rep_type_##]">
      <s_article_related_rep_thumbnail>
      <div class="related-post-thumb">
        <img src="[##_article_related_rep_thumbnail_link_##]" alt="" loading="lazy">
      </div>
      </s_article_related_rep_thumbnail>
      <span class="related-post-title">[##_article_related_rep_title_##]</span>
      <span class="related-post-date">[##_article_related_rep_date_##]</span>
    </a>
    </s_article_related_rep>
  </div>
</section>
</s_article_related>
```

### 댓글

```html
<s_rp>
<section class="comments-section" aria-label="댓글">
  <h2 class="comments-heading">댓글</h2>
  [##_comment_group_##]
</section>
</s_rp>
```

- `[##_comment_group_##]` : 티스토리가 댓글 UI 전체(입력창 포함)를 자동으로 생성해 삽입

---

## 10. PROTECTED — 비밀글

```html
<s_article_protected>
<s_permalink_article_rep>
<article class="post-detail">
  <div class="post-content">
    <div class="protected-area">
      <p class="protected-message">비밀번호로 보호되어 있는 글입니다.</p>
      <form class="protected-form" onsubmit="[##_article_dissolve_##]">
        <input type="password" id="[##_article_password_##]" name="[##_article_password_##]"
               placeholder="비밀번호를 입력하세요" />
        <button type="submit">확인</button>
      </form>
    </div>
  </div>
</article>
</s_permalink_article_rep>
</s_article_protected>
```

- `<s_article_protected>` : 현재 글이 비밀글일 때만 이 블록을 출력
- `<input type="password">` : 입력값을 `*`로 가리는 비밀번호 입력 필드
- `[##_article_dissolve_##]` : 비밀번호를 검증하는 티스토리 함수 호출로 교체

---

## 11. PAGE REP — 페이지 타입 글

```html
<s_page_rep>
<s_permalink_article_rep>
<article class="post-detail" itemscope itemtype="http://schema.org/Article">
  <header class="post-detail-header">
    <span class="post-category">공지사항</span>
    <time class="post-date">[##_article_rep_date_##]</time>
    <h1 class="post-detail-title">[##_article_rep_title_##]</h1>
  </header>
  <div class="post-content">[##_article_rep_desc_##]</div>
</article>
</s_permalink_article_rep>
</s_page_rep>
```

- `<s_page_rep>` : 카테고리 없이 별도로 만드는 "페이지 타입" 글일 때 출력 (예: 소개 페이지)

---

## 12. PAGING — 페이지네이션

```html
<s_paging>
<nav class="pagination" aria-label="페이지 탐색">
  <a [##_prev_page_##] class="page-btn page-prev">
    <svg ...></svg>
  </a>
  <span class="page-numbers">
    <s_paging_rep>
    <a [##_paging_rep_link_##] class="page-num">[##_paging_rep_link_num_##]</a>
    </s_paging_rep>
  </span>
  <a [##_next_page_##] class="page-btn page-next">
    <svg ...></svg>
  </a>
</nav>
</s_paging>
```

- `<s_paging>` : 글이 여러 페이지에 걸쳐 있을 때만 페이지네이션 출력
- `[##_prev_page_##]` : `href="URL"` 형태로 교체 (이전 페이지 링크 속성 전체)
- `<s_paging_rep>` : 각 페이지 번호마다 반복. 현재 페이지는 CSS `.on` 클래스가 자동으로 붙음
- `[##_paging_rep_link_num_##]` : 페이지 번호 숫자로 교체

---

## 13. TAG / LOCAL / GUEST — 기타 페이지

### 태그 클라우드

```html
<s_tag>
<div class="tag-cloud-page">
  <h2 class="list-page-title">태그</h2>
  <div class="tag-cloud">
    <s_tag_rep>
    <a href="[##_tag_link_##]" class="tag-item [##_tag_class_##]">[##_tag_name_##]</a>
    </s_tag_rep>
  </div>
</div>
</s_tag>
```

- `[##_tag_class_##]` : 태그 사용 빈도에 따라 `cloud1` ~ `cloud5` 클래스로 교체 (CSS에서 크기 차별화)

### 위치로그

```html
<s_local>
<div class="tag-cloud-page">
  <h2>위치로그</h2>
  <s_local_spot_rep>
    <p class="local-spot">[##_local_spot_##]</p>
  </s_local_spot_rep>
  <s_local_info_rep>
    <p class="local-info" style="padding-left:[##_local_info_depth_##]px">
      <a href="[##_local_info_link_##]">[##_local_info_title_##]</a>
    </p>
  </s_local_info_rep>
</div>
</s_local>
```

### 방명록

```html
<s_guest>
<div class="guestbook-page">
  <h2>방명록</h2>
  [##_guestbook_group_##]
</div>
</s_guest>
```

- `[##_guestbook_group_##]` : 방명록 UI 전체를 티스토리가 자동 삽입

---

## 14. SIDEBAR — 사이드바

### 사이드바 래퍼

```html
<aside class="site-sidebar" id="siteSidebar" aria-label="사이드바">
  <s_sidebar>
    <s_sidebar_element>
      <!-- 위젯 하나 -->
    </s_sidebar_element>
  </s_sidebar>
</aside>
```

- `<s_sidebar>` : 사이드바 영역 전체 래퍼
- `<s_sidebar_element>` : 사이드바 위젯 하나씩을 감싸는 단위. 여러 개 사용 가능

### 프로필 위젯

```html
<s_sidebar_element>
<div class="sidebar-widget sidebar-profile">
  <div class="sidebar-profile-avatar">[##_blog_image_##]</div>
  <p class="sidebar-profile-name">[##_blogger_##]</p>
  <p class="sidebar-profile-desc">[##_desc_##]</p>
  <div class="profile-subscribe-wrap">
    [##_subscription_button_##]
  </div>
  <div class="profile-admin-btns [##_role_group_##]">
    <button class="profile-admin-btn btn-write">글쓰기</button>
    <button class="profile-admin-btn btn-blog-manage">블로그 관리</button>
  </div>
</div>
</s_sidebar_element>
```

- `[##_blog_image_##]` : 블로그 대표 이미지(`<img>` 태그)로 교체
- `[##_blogger_##]` : 블로그 운영자 이름으로 교체
- `[##_subscription_button_##]` : 구독 버튼 HTML로 교체
- `[##_role_group_##]` : 접속자 권한에 따라 `owner`, `member`, `guest` 등으로 교체
  - CSS에서 `.profile-admin-btns.owner { display: flex; }`로 관리자일 때만 버튼 표시

### TOC(목차) 위젯

```html
<div class="sidebar-widget sidebar-toc" id="tocWidget" aria-label="목차">
  <h3 class="sidebar-widget-title">목차</h3>
  <nav class="toc-nav" id="tocNav"></nav>
</div>
```

- CSS에서 기본 `display: none`으로 숨겨져 있음
- JavaScript가 글 본문에서 `<h2>`, `<h3>` 태그를 찾아 목차를 자동 생성하고 표시

### 카테고리 위젯

```html
<s_sidebar_element>
<div class="sidebar-widget sidebar-category">
  <h3 class="sidebar-widget-title">CATEGORIES</h3>
  [##_category_list_##]
</div>
</s_sidebar_element>
```

- `[##_category_list_##]` : 티스토리가 카테고리 트리 HTML 전체를 생성해 삽입

### 최근글 위젯

```html
<s_sidebar_element>
<div class="sidebar-widget">
  <h3 class="sidebar-widget-title">RECENT POSTS</h3>
  <ul class="sidebar-recent-list">
    <s_rctps_rep>
    <li class="sidebar-recent-item">
      <a href="[##_rctps_rep_link_##]" class="sidebar-recent-link">
        <span class="sidebar-recent-title">[##_rctps_rep_title_##]</span>
        <span class="sidebar-recent-date">[##_rctps_rep_simple_date_##]</span>
      </a>
    </li>
    </s_rctps_rep>
  </ul>
</div>
</s_sidebar_element>
```

- `<s_rctps_rep>` : 최근 게시글 수(index.xml `<recentEntries>` 값)만큼 반복

### 방문자 카운터 위젯

```html
<div class="sidebar-widget">
  <h3 class="sidebar-widget-title">VISITORS</h3>
  <div class="sidebar-counter">
    <div class="sidebar-counter-item">
      <span class="sidebar-counter-label">Total</span>
      <span class="sidebar-counter-value">[##_count_total_##]</span>
    </div>
    <div class="sidebar-counter-item">
      <span>Today</span>
      <span>[##_count_today_##]</span>
    </div>
    <div class="sidebar-counter-item">
      <span>Yesterday</span>
      <span>[##_count_yesterday_##]</span>
    </div>
  </div>
</div>
```

---

## 15. FOOTER — 푸터

```html
<footer class="site-footer">
  <div class="footer-inner">
    <p class="footer-copy">
      &copy; <span id="footerYear"></span> [##_blogger_##].
      Powered by <a href="https://www.tistory.com">Tistory</a>.
    </p>
    <nav class="footer-nav" aria-label="푸터 내비게이션">
      <a href="[##_rss_url_##]" class="footer-link">RSS</a>
      <a href="[##_taglog_link_##]" class="footer-link">태그</a>
      <a href="[##_guestbook_link_##]" class="footer-link">방명록</a>
    </nav>
  </div>
</footer>
```

- `<footer>` : 페이지 하단 영역을 나타내는 시맨틱 태그
- `&copy;` : HTML 특수문자. 저작권 기호 `©`를 나타냄
- `<span id="footerYear">` : JavaScript가 현재 연도를 이 안에 삽입
- `<nav aria-label="푸터 내비게이션">` : 헤더 `<nav>`와 구분하기 위해 `aria-label`로 명칭 지정

---

## 16. SCRIPT — 자바스크립트

모든 HTML이 로드된 뒤 실행되도록 `</body>` 직전에 위치합니다.

### 기능별 코드 설명

#### 1) 저작권 연도 자동 갱신
```javascript
var yearEl = document.getElementById('footerYear');
if (yearEl) yearEl.textContent = new Date().getFullYear();
```
- `document.getElementById` : `id` 로 요소를 찾음
- `new Date().getFullYear()` : 현재 연도를 숫자로 반환

#### 2) 다크/라이트 테마 토글
```javascript
themeToggle.addEventListener('click', function () {
  var next = document.documentElement.dataset.theme === 'dark' ? 'light' : 'dark';
  document.documentElement.dataset.theme = next;
  localStorage.setItem('atm-theme', next);
});
```
- `addEventListener('click', ...)` : 클릭 이벤트가 발생하면 함수를 실행
- 삼항 연산자 `조건 ? 참 : 거짓` : 현재가 dark면 light로, 아니면 dark로
- `localStorage.setItem` : 선택한 테마를 브라우저에 저장 (새로고침 후에도 유지)

#### 3) 읽기 진행 바
```javascript
window.addEventListener('scroll', function () {
  var st = window.pageYOffset;  // 현재 스크롤 위치
  var dh = document.documentElement.scrollHeight - document.documentElement.clientHeight;
  progressBar.style.width = (dh > 0 ? Math.min(st / dh * 100, 100) : 0) + '%';
}, { passive: true });
```
- `{ passive: true }` : 스크롤 성능 최적화 옵션. 이 이벤트 핸들러에서 스크롤을 막지 않음을 브라우저에 알림

#### 4) 모바일 사이드바 토글
```javascript
mobileBtn.addEventListener('click', function () {
  var open = sidebar.classList.toggle('is-open');
  document.body.classList.toggle('sidebar-open', open);
  mobileBtn.setAttribute('aria-expanded', String(open));
});
```
- `classList.toggle('is-open')` : 클래스가 있으면 제거, 없으면 추가. 반환값은 추가됐으면 `true`
- `setAttribute('aria-expanded', ...)` : 드롭다운 열림/닫힘 상태를 접근성 속성에 업데이트

#### 5) 검색 드롭다운
```javascript
searchToggle.addEventListener('click', function (e) {
  e.stopPropagation();  // 클릭 이벤트가 document까지 전파되지 않도록 차단
  var open = searchDropdown.classList.toggle('is-open');
  if (open) searchDropdown.querySelector('.search-input').focus();
});
```
- `e.stopPropagation()` : 이 클릭이 바깥으로 전파되면 바로 닫히기 때문에 전파를 막음
- `.focus()` : 드롭다운이 열리면 입력창에 커서를 자동으로 이동

#### 6) TOC(목차) 자동 생성
```javascript
var headings = Array.prototype.slice.call(postContent.querySelectorAll('h2, h3'));
if (headings.length >= 2) {
  tocWidget.style.display = 'block';
  // 각 heading에 id 부여 → <a href="#id"> 링크 생성
  headings.forEach(function (h) {
    if (!h.id) h.id = 'toc-' + (counter++);
  });
  // IntersectionObserver로 스크롤 위치에 따라 active 클래스 갱신
}
```
- `querySelectorAll('h2, h3')` : 글 본문의 모든 h2, h3 태그를 배열로 수집
- `IntersectionObserver` : 요소가 화면에 보이는지 감지하는 최신 Web API. scroll 이벤트보다 성능 우수
