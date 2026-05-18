# index.xml 스터디 가이드

> **학습 목표:** index.xml이 티스토리에서 어떤 역할을 하는지, 각 태그가 무엇을 설정하는지 이해합니다.
>
> **학습 수준:** XML/HTML 기초 지식 보유자 대상.

---

## 목차
1. [XML이란?](#1-xml이란)
2. [전체 파일 구조](#2-전체-파일-구조)
3. [information — 스킨 기본 정보](#3-information--스킨-기본-정보)
4. [author — 제작자 정보](#4-author--제작자-정보)
5. [default — 기본값 설정](#5-default--기본값-설정)
6. [tree — 카테고리 트리 색상](#6-tree--카테고리-트리-색상)
7. [variables — 스킨 커스텀 옵션](#7-variables--스킨-커스텀-옵션)
8. [index.xml 수정하기](#8-indexxml-수정하기)

---

## 1. XML이란?

> **XML(eXtensible Markup Language)** 은 데이터를 구조화해서 저장하는 텍스트 형식입니다.
> HTML처럼 태그(`< >`)를 사용하지만, 브라우저에 표시하는 것이 아닌 **설정값 전달**이 목적입니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
```

- 첫 줄: "이 파일은 XML 1.0 버전, UTF-8 인코딩입니다"라고 선언
- 브라우저에 표시되지 않는 메타 선언

### HTML vs XML 차이

| 구분 | HTML | XML |
|------|------|-----|
| 목적 | 화면 표시 | 데이터 저장/전달 |
| 태그 | 정해진 태그만 사용 | 사용자 정의 태그 가능 |
| 대소문자 | 대소문자 무관 | 대소문자 구분 |
| 닫는 태그 | 생략 가능한 경우 있음 | 반드시 닫아야 함 |

---

## 2. 전체 파일 구조

```xml
<?xml version="1.0" encoding="utf-8"?>
<skin>

  <information>   <!-- 스킨 이름, 버전, 설명, 라이선스 -->
    ...
  </information>

  <author>         <!-- 제작자 이름, 홈페이지, 이메일 -->
    ...
  </author>

  <default>        <!-- 사이드바 위젯 기본값, 색상, 개수 등 -->
    ...
  </default>

  <variables>      <!-- 스킨 관리 페이지에서 사용자가 설정할 수 있는 옵션 -->
    ...
  </variables>

</skin>
```

- `<skin>` : 루트(최상위) 태그. 모든 내용을 감쌈
- XML은 반드시 **하나의 루트 태그**만 가져야 함

---

## 3. information — 스킨 기본 정보

```xml
<information>
  <name>Yangne-Throwing_Apple</name>
  <version>1.0</version>
  <description>
    <![CDATA[Yangne-Throwing_Apple 스킨입니다. 라이트/다크 모드, 반응형 레이아웃, 플로팅 목차(TOC)를 지원합니다.]]>
  </description>
  <license>
    <![CDATA[자유롭게 수정이 가능하며, 저작권 표시 하에 재배포 가능합니다.]]>
  </license>
</information>
```

### 핵심 태그 설명

- `<name>` : 티스토리 스킨 등록 화면에 표시되는 스킨 이름
- `<version>` : 스킨 버전 번호. 업데이트 시 구분용
- `<description>` : 스킨 설명
- `<license>` : 이 스킨의 사용/배포 조건

### `<![CDATA[ ... ]]>` 란?

> CDATA(Character Data) 섹션. 이 안의 내용은 XML 태그로 해석하지 않고 **순수 텍스트**로 처리합니다.

```xml
<!-- 문제: XML 파서가 < 를 태그 시작으로 오해 -->
<description>a < b 라면 처리됩니다</description>  ← 오류 발생

<!-- 해결: CDATA로 감싸면 안전 -->
<description><![CDATA[a < b 라면 처리됩니다]]></description>  ← 정상
```

- `<`, `>`, `&` 같은 특수문자가 포함된 텍스트를 안전하게 저장할 때 사용
- 이 스킨에서는 한글 설명 텍스트를 안전하게 담기 위해 사용

---

## 4. author — 제작자 정보

```xml
<author>
  <name>Yangne-Throwing_Apple</name>
  <homepage></homepage>
  <email></email>
</author>
```

- `<homepage>`, `<email>` : 현재 비어 있음. 입력하면 티스토리가 제작자 정보로 표시
- 스킨 동작에 영향을 주지 않는 메타 정보

---

## 5. default — 기본값 설정

티스토리가 사이드바 위젯들을 렌더링할 때 사용하는 기본값들을 정의합니다.

```xml
<default>
  <recentEntries>5</recentEntries>
  <recentComments>5</recentComments>
  <recentTrackbacks>5</recentTrackbacks>
  <itemsOnGuestbook>10</itemsOnGuestbook>
  <tagsInCloud>30</tagsInCloud>
  <sortInCloud>3</sortInCloud>
  <expandComment>0</expandComment>
  <expandTrackback>0</expandTrackback>
  <lengthOfRecentNotice>25</lengthOfRecentNotice>
  <lengthOfRecentEntry>27</lengthOfRecentEntry>
  <lengthOfRecentComment>30</lengthOfRecentComment>
  <lengthOfRecentTrackback>30</lengthOfRecentTrackback>
  <lengthOfLink>30</lengthOfLink>
  <showListOnCategory>1</showListOnCategory>
  <showListOnArchive>1</showListOnArchive>
  <commentMessage>...</commentMessage>
  <trackbackMessage>...</trackbackMessage>
  <contentWidth>800</contentWidth>
  <tree>...</tree>
</default>
```

### 각 설정값 설명

| 태그 | 값 | 의미 |
|------|-----|------|
| `<recentEntries>` | `5` | 사이드바 "최근 글" 위젯에 표시할 글 수 |
| `<recentComments>` | `5` | "최근 댓글" 위젯에 표시할 댓글 수 |
| `<recentTrackbacks>` | `5` | "최근 트랙백" 표시 수 |
| `<itemsOnGuestbook>` | `10` | 방명록 페이지당 댓글 수 |
| `<tagsInCloud>` | `30` | 태그 클라우드에 표시할 최대 태그 수 |
| `<sortInCloud>` | `3` | 태그 정렬 방식 (3 = 사용 빈도순) |
| `<expandComment>` | `0` | 댓글을 기본적으로 펼쳐 표시할지 (0 = 접음) |
| `<expandTrackback>` | `0` | 트랙백을 기본적으로 펼쳐 표시할지 |
| `<lengthOfRecentNotice>` | `25` | 최근 공지사항 제목 표시 글자 수 |
| `<lengthOfRecentEntry>` | `27` | 최근 글 제목 표시 글자 수 |
| `<lengthOfRecentComment>` | `30` | 최근 댓글 표시 글자 수 |
| `<lengthOfLink>` | `30` | 링크 제목 표시 글자 수 |
| `<showListOnCategory>` | `1` | 카테고리 클릭 시 목록 표시 (1 = 표시) |
| `<showListOnArchive>` | `1` | 아카이브 클릭 시 목록 표시 |
| `<contentWidth>` | `800` | 글 본문 최대 너비 (px). CSS `--max-prose`와 연동 |

### 댓글 메시지

```xml
<commentMessage>
  <none>댓글이 없습니다.</none>
  <single>댓글 &lt;span class="cnt"&gt;하나&lt;/span&gt; 달렸습니다.</single>
</commentMessage>
```

- `<none>` : 댓글이 0개일 때 표시되는 문자열
- `<single>` : 댓글이 1개일 때 표시되는 문자열
- `&lt;` = `<`, `&gt;` = `>` : XML에서 꺾쇠 기호를 안전하게 쓰는 방법 (HTML 특수문자와 동일)

---

## 6. tree — 카테고리 트리 색상

```xml
<tree>
  <color>1D1D1F</color>
  <bgColor>FBFBFD</bgColor>
  <activeColor>007AFF</activeColor>
  <activeBgColor>EAF3FF</activeBgColor>
  <labelLength>27</labelLength>
  <showValue>1</showValue>
</tree>
```

- 티스토리 카테고리 위젯(`[##_category_list_##]`)의 기본 색상을 설정
- 이 값들은 CSS에서 덮어쓸 수 있으며, 이 스킨의 `style.css`에서 `.sidebar-category` 섹션이 대부분 오버라이드

| 태그 | 값 | 의미 |
|------|-----|------|
| `<color>` | `1D1D1F` | 카테고리 텍스트 색 (진한 검정) |
| `<bgColor>` | `FBFBFD` | 카테고리 위젯 배경색 |
| `<activeColor>` | `007AFF` | 선택된 카테고리 텍스트 색 (파란색) |
| `<activeBgColor>` | `EAF3FF` | 선택된 카테고리 배경색 (연한 파란색) |
| `<labelLength>` | `27` | 카테고리 이름 최대 표시 글자 수 |
| `<showValue>` | `1` | 글 수 표시 여부 (1 = 표시) |

**참고:** 색상값은 `#` 없이 HEX 코드만 입력합니다.

---

## 7. variables — 스킨 커스텀 옵션

```xml
<variables>
  <variablegroup name="히어로 이미지">
    <variable>
      <name>cover-image</name>
      <label><![CDATA[히어로 배경 이미지]]></label>
      <type>IMAGE</type>
      <option />
      <default><![CDATA[]]></default>
      <description>
        <![CDATA[메인 페이지 상단 히어로 섹션의 배경 이미지입니다. 미설정 시 기본 그라데이션이 표시됩니다.]]>
      </description>
    </variable>
  </variablegroup>
</variables>
```

### 구조 설명

```
<variables>                       ← 변수 목록 전체
  <variablegroup name="그룹명">   ← 관련 변수를 묶는 그룹 (관리 UI에서 섹션 제목)
    <variable>                    ← 변수 하나
      <name>변수이름</name>       ← skin.html에서 [##_var_변수이름_##]으로 참조
      <label>표시 이름</label>    ← 관리 페이지에서 보이는 한국어 이름
      <type>타입</type>           ← 입력 유형
      <option />                  ← 추가 옵션 (이 스킨에서는 비어 있음)
      <default>기본값</default>   ← 설정 안 했을 때의 초기값
      <description>설명</description> ← 관리 페이지에서 보이는 안내 문구
    </variable>
  </variablegroup>
</variables>
```

### variable `<type>` 종류

| 타입 | 의미 |
|------|------|
| `STRING` | 텍스트 한 줄 |
| `TEXT` | 여러 줄 텍스트 |
| `COLOR` | 색상 선택기 |
| `IMAGE` | 이미지 업로드 |
| `INTEGER` | 정수 입력 |
| `BOOLEAN` | 참/거짓 토글 |

### skin.html에서 어떻게 쓰이나?

```html
<!-- index.xml에서 name을 "cover-image"로 정의했으므로 -->
<s_if_var_cover-image>
<style>
  .hero-bg { background-image: url('[##_var_cover-image_##]') !important; }
</style>
</s_if_var_cover-image>
```

- `[##_var_cover-image_##]` : 사용자가 관리 페이지에서 업로드한 이미지 URL로 교체
- `<s_if_var_cover-image>` : 이 변수에 값이 있을 때만 내부 코드를 출력

---

## 8. index.xml 수정하기

### 스킨 설명 바꾸기

```xml
<information>
  <name>내 블로그 스킨 이름</name>     ← 원하는 이름으로 변경
  <version>1.1</version>               ← 버전 올리기
  <description>
    <![CDATA[나만의 설명을 입력하세요.]]>
  </description>
</information>
```

### 사이드바 최근 글 수 늘리기

```xml
<default>
  <recentEntries>10</recentEntries>    ← 5에서 10으로 변경
</default>
```

### 히어로 이미지 설정 추가

현재 `cover-image` 하나만 있습니다. 새 변수를 추가하려면:

```xml
<variablegroup name="색상 설정">
  <variable>
    <name>accent-color</name>
    <label><![CDATA[강조 색상]]></label>
    <type>COLOR</type>
    <option />
    <default><![CDATA[#007AFF]]></default>
    <description><![CDATA[링크, 버튼 등에 사용되는 강조 색상입니다.]]></description>
  </variable>
</variablegroup>
```

그리고 skin.html에서 사용:
```html
<s_if_var_accent-color>
<style>:root { --color-accent: [##_var_accent-color_##]; }</style>
</s_if_var_accent-color>
```

---

## 정리: 세 파일의 관계

```
index.xml           skin.html                   style.css
────────────        ─────────────────────       ─────────────────────
스킨 설정값 정의    HTML 구조 + 티스토리 치환자   시각적 스타일 정의
                         ↑                             ↑
                    index.xml의 variables        skin.html의 class="..."
                    → [##_var_이름_##]           → .class-name { ... }
                    → <s_if_var_이름> 조건
```

- **index.xml** : 블로그 관리자가 설정할 수 있는 옵션과 기본값을 티스토리에 알려줌
- **skin.html** : 티스토리 치환자로 실제 데이터를 받아 HTML 구조를 만들고, CSS 클래스로 스타일 연결
- **style.css** : HTML 요소에 색상/크기/레이아웃 등 시각적 스타일을 입힘
