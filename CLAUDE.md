# CLAUDE.md — 수업 모션 영상 하네스

## 목적
교과서 소단원 하나를 넣으면, 선생님이 고른 레퍼런스의 **룩(책상 위 모눈종이)과 움직임(연필로 그려 가기)**으로 교실 TV용 수업 영상을 만든다.
시작: `수업 영상 만들자` → `.claude/skills/make-video/SKILL.md` 순서를 따른다.

## 규칙 3개
1. **내용은 교과서에서만, 쪽수와 함께.** 화면 글 · 질문 · 정리는 `docs/textbook/*.md` 에 있는 문장에서만 가져오고, 가져온 곳마다 `p.○` 를 단다. 교과서 문장은 글자 · 띄어쓰기 · 문장부호까지 그대로 (`docs/video.md` 5장).
2. **값은 `docs/` 와 `src/parts/` 에서만.** 색 · 글꼴 · 크기는 `docs/design.md`, 움직임 · 시간은 `docs/motion.md`, 화면 규칙은 `docs/video.md`, 모양은 `src/parts/`. docs 의 값은 모두 `references/` 에서 잰 것이다. **문서에 없는 값은 지어내지 말고 선생님께 묻는다** — 필요하면 `references/` 에서 재서 근거(파일 · 초)를 붙여 "새 후보"로 묻고, 승인되면 해당 docs 에 먼저 적은 뒤 쓴다.
3. **사람이 승인한 뒤에 만들고, 판정은 critic 이 한다.** ✋ 단계(교과서 정리 · 장면표 · 스냅보드)는 선생님이 "좋아요"라고 해야 다음으로 간다. 만든 것이 통과인지는 critic 만 정하고, critic 은 고치지 않는다.

## 폴더
| 폴더 · 파일 | 무엇 |
|---|---|
| `docs/textbook/` | 교과서 소단원 md (원문, 쪽수 달림) · `_format.md` 형식 · `index.md` 목차 |
| `docs/design.md` | 룩: 색 · 글자 · 크기 · 질감 · 그림 규칙 (출처: `references/j-uni/`) |
| `docs/motion.md` | 움직임: 시간 · 가감속 · 거리 · 부품별 순서 · 머무는 시간 · 카메라 (출처: ref8 영상) |
| `docs/video.md` | 교실 TV 화면 규칙: 최소 글자 · 배경 · 글 길이 · 화면 틀 · 표기 · 부품 쓰는 법 |
| `src/parts/` | 부품 html 8개 + `tokens.css` · `_check/` 견본 그림 |
| `.claude/skills/hyperframes*` | HyperFrames 사용법 (설치된 스킬). 계약 · 명령만 따르고, 이야기 고르기 · SPEC · 음악 기본값은 이 하네스 순서가 대신한다 |
| `src/assets/` | 글꼴(`fonts/`) · 사진(`photos/` + `SOURCES.md`) |
| `references/j-uni/` | 레퍼런스 원본(올리지 않음) + `README.md` 분석 |
| `templates/look/` | 룩 빈 양식 (새 룩을 만들 때만) |
| `.claude/agents/` | content-editor · art-director · director · builder · critic |
| `.claude/skills/make-video/` | 영상 한 편 만드는 순서 |
| `out/<영상이름>/` | 영상 한 편의 모든 작업물 (올리지 않음) |

## 고정 · 참조 · 금지
- **고정 (바꾸지 않음 — 바꾸려면 선생님 승인):** `docs/design.md` · `docs/motion.md` · `docs/video.md` · `src/parts/` · `src/assets/fonts/` · `docs/textbook/` 의 교과서 md.
- **참조 (읽기만):** `references/` · `docs/textbook/` · `templates/` · `.claude/skills/hyperframes*` (HyperFrames 사용법).
- **금지:**
  - 교과서에 없는 내용 · 쪽수 없는 문장을 화면에 넣기, 교과서 문장을 고쳐 쓰기
  - 문서에 없는 색 · 크기 · 시간 · 가감속을 지어내기 (비슷한 값으로 "대충" 맞추기 포함)
  - 레퍼런스의 그림 · 글자 · 사진 · 로고 · 소리를 가져오기 (느낌과 움직임만)
  - 교과서 그림을 그대로 넣기
  - ✋ 단계에서 승인 없이 다음으로 넘어가기 · critic 판정 없이 렌더하기
  - 교과서 변환본(`docs/textbook/*.md`, 형식 · 목차 · 예시 빼고)과 `out/` 을 커밋하기
  - 강원교육현옥샘 글꼴(`src/assets/fonts/GangwonEduHyeonok.ttf`)을 라이선스 확인 전에 공개 저장소로 올리기

## 작업 순서 (영상 한 편)
| 단계 | 누가 | 만드는 것 | 멈춤 |
|---|---|---|---|
| 0 브리프 | 메인 | `out/<영상이름>/brief.md` | 질문에 답을 받을 때까지 |
| 1 교과서 정리 | content-editor | `content.md` | ✋ 선생님 승인 |
| 2 레퍼런스 | art-director | `look.md` | 질문이 있을 때만 |
| 3 장면표 | director | `scenes.md` | ✋ 선생님 승인 |
| 4 스냅보드 | builder → critic | `snapboard/` + `review-snapboard.md` | ✋ 선생님 승인 |
| 5 생성 · 검수 | builder ↔ critic | HyperFrames 프로젝트 + `review.md` | critic PASS 까지 (3번 넘게 FAIL 이면 선생님께) |
| 6 렌더 | builder | `<영상이름>.mp4` | 미리보기 확인 뒤 |
| 7 규칙 남기기 | 메인 | 아래 "쌓인 규칙" 또는 해당 docs | 선생님 승인 |

자세한 순서와 각 단계의 질문은 `.claude/skills/make-video/SKILL.md`.

## 쌓인 규칙
영상을 만들며 선생님이 승인한 새 규칙을 날짜와 함께 여기에 한 줄씩 남긴다. 값(색 · 시간 등)이 바뀌는 규칙은 여기가 아니라 해당 docs 를 고친다.

- 2026-11-15 · 글자가 써지는 시간은 어림 폭이 아니라 스냅보드에서 잰 실제 글자 폭 ÷ `write-speed`(650px/s)로 셈한다. builder 가 스냅보드 때 글자 폭을 `measure.json` 에 재 두고 director 가 그 값을 쓴다 (7-1-robot-basics).
