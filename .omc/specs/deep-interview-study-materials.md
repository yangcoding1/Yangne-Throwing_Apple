# Deep Interview Spec: TSTORY_SKIN 스터디 자료 제작

## Metadata
- Interview ID: study-materials-2026-05-18
- Rounds: 4
- Final Ambiguity Score: 16%
- Type: brownfield
- Generated: 2026-05-18
- Threshold: 0.20
- Initial Context Summarized: no
- Status: PASSED

## Clarity Breakdown
| 차원 | 점수 | 가중치 | 가중 점수 |
|------|------|--------|---------|
| Goal Clarity | 0.85 | 35% | 0.30 |
| Constraint Clarity | 0.80 | 25% | 0.20 |
| Success Criteria | 0.85 | 25% | 0.21 |
| Context Clarity | 0.85 | 15% | 0.13 |
| **Total Clarity** | | | **0.84** |
| **Ambiguity** | | | **16%** |

## Goal
`skin.html`, `style.css`, `index.xml` 3개 파일에 대해 **파일당 1개의 스터디 MD 파일**을 제작한다.  
각 MD 파일은 소스 코드를 **섹션(기능 영역) 단위**로 나누어, 기초 지식만 있는 학습자가 코드를 읽고 해석할 수 있도록 설명한다.

## Constraints
- 대상 독자: HTML/CSS 완전 기초 수준 (태그와 속성 개념은 알지만, 실무 패턴은 처음)
- 학습 파일 수: 3개 (skin.html 가이드, style.css 가이드, index.xml 가이드)
- 섹션 구성: 파일의 실제 구조 순서대로 위에서 아래로 설명
- 언어: 한국어
- 설명 스타일: 섹션 제목 + 역할 설명 + 코드 블록 + 핵심 태그/속성 불릿 리스트

## Non-Goals
- 새로운 코드 작성 또는 수정
- 연습 문제나 퀴즈 포함
- 영어 설명 생성
- 티스토리 스킨 등록 방법 안내 (APPLY_GUIDE.md에 이미 있음)

## Acceptance Criteria
- [ ] `study/skin.html_가이드.md` 생성: skin.html 전체를 섹션별로 설명
- [ ] `study/style.css_가이드.md` 생성: style.css 전체를 섹션별로 설명
- [ ] `study/index.xml_가이드.md` 생성: index.xml 구조 설명
- [ ] 각 섹션은 "역할 설명 → 코드 블록 → 핵심 요소 불릿" 형식을 따름
- [ ] 티스토리 고유 태그(`s_t1`, `s_article`, `s_sidebar_element` 등)는 반드시 별도로 설명
- [ ] CSS `--변수` (Custom Properties) 사용 부분은 개념과 함께 설명
- [ ] 기초 학습자가 읽었을 때 각 코드 블록의 역할을 설명할 수 있는 수준

## Assumptions Exposed & Resolved
| 가정 | 질문 | 결정 |
|------|------|------|
| 일부 파일만 다룰 것 | 어떤 부분에 집중? | 전체 파일 전부 |
| 개념별 구성이 나을 수 있다 | 구성 방식은? | 파일별 1개, 섹션 순서대로 |
| 설명 깊이가 불명확 | 설명 스타일은? | 섹션별 요약 + 핵심 요소 리스트 |

## Technical Context
- `skin.html`: 31KB, Tistory 치환자(`s_*` 태그, `##변수##`) + 일반 HTML 혼합
- `style.css`: 36KB, CSS Custom Properties(`:root`), Flexbox/Grid, 다크모드(@media) 포함
- `index.xml`: 스킨 메타데이터 (이름, 버전, 미리보기 이미지 경로)
- `document-tistory-skin/`: 티스토리 API 레퍼런스 (설명 작성 시 참조 가능)

## Ontology (Key Entities)
| 엔티티 | 유형 | 필드 | 관계 |
|--------|------|------|------|
| StudyMaterial | core domain | file_name, sections | contains CodeSection |
| SourceCode | external | file_path, size_kb | referenced by StudyMaterial |
| Learner | supporting | knowledge_level=basic | consumes StudyMaterial |
| CodeSection | supporting | heading, description, code_block, bullet_list | part of StudyMaterial |

## Interview Transcript
<details>
<summary>전체 Q&A (4 라운드)</summary>

### Round 1
**Q:** 스터디 자료를 다 보고 나서 어떤 상태가 되어있으면 '성공'이라고 느낄 것 같나요?
**A:** 코드 해석 가능
**Ambiguity:** 41%

### Round 2
**Q:** skin.html과 style.css는 각각 31KB, 36KB로 분량이 많습니다. 어떤 부분을 중심으로 다뤄야 할까요?
**A:** 전체 파일 전부
**Ambiguity:** 34%

### Round 3
**Q:** 스터디 MD 파일을 어떤 식으로 구성하면 보기 좋을까요?
**A:** 파일 별 1개씩 (파일 위에서 아래로 섹션별 설명)
**Ambiguity:** 24%

### Round 4
**Q:** 코드 설명 스타일은 어떻게 하면 보기 좋을까요?
**A:** 섹션별 설명 (섹션 제목 + 설명 + 코드 블록 + 핵심 태그/속성 불릿)
**Ambiguity:** 16% ✅

</details>
