---
name: make-video
description: 교과서 소단원 하나로 교실 TV용 수업 모션 영상 한 편을 만드는 순서. "수업 영상 만들자", "○○ 단원 영상 만들어줘"처럼 수업 영상을 새로 만들자고 할 때 쓴다. 브리프 → 교과서 정리 ✋ → 레퍼런스 → 장면표 ✋ → 스냅보드 ✋ → 생성 · 검수 → 렌더 → 규칙 남기기.
---

# make-video — 수업 영상 한 편 만들기

`CLAUDE.md` 의 규칙 3개를 따른다: **내용은 교과서에서만(쪽수와 함께) · 값은 docs 와 src/parts 에서만 · 승인 뒤에 만들고 critic 이 판정.**
룩과 움직임 값은 `docs/design.md` · `docs/motion.md` · `docs/video.md` · `src/parts/` 에서만 가져온다 (docs 의 값은 `references/` 에서 잰 것). **문서에 없는 값은 지어내지 말고 선생님께 묻는다** — 필요하면 `references/` 에서 재서 근거를 붙여 새 후보로 묻고, 승인되면 docs 에 먼저 적는다.

✋ = 선생님이 "좋아요"(또는 고칠 점)를 말할 때까지 멈춘다. 고칠 점을 받으면 그 단계를 다시 하고 다시 ✋.
모든 작업물은 `out/<영상이름>/` 에 둔다 (저장소에 올라가지 않음). 영상이름은 영어 소문자 · 하이픈 (예: `6-1-data-kinds`).

## 0. 브리프 (메인)
선생님께 한 번에 묻는다. 기본값이 있는 것은 기본값을 같이 보여 준다.
1. 어느 소단원 · 몇 쪽? (`docs/textbook/index.md` 목차를 보여 줌)
2. 영상 길이는? (기본값: `docs/video.md` 4장 "영상 길이" — 2분 안팎)
3. 내레이션 · 음악 · 효과음을 넣을까? (기본값 없음 — 꼭 묻는다. HyperFrames 스킬의 "15초 넘는 영상은 음악" 기본값을 쓰지 않는다)
4. 영상 이름 (기본값: 소단원 번호 + 영어 낱말)
→ `out/<영상이름>/brief.md` 에 답을 적는다.

## 1. 교과서 정리 ✋ (content-editor)
- `content-editor` 를 부른다 → `out/<영상이름>/content.md`.
- 선생님께 보여 줄 것: 핵심 개념 2~4개 · 장면 후보 목록(소제목 · 쪽) · 정리 질문 후보 · 뺀 것 · 질문.
- ✋ 승인을 받으면 content.md 맨 위에 `승인: <날짜>` 를 적는다.

## 2. 레퍼런스 (art-director)
- `art-director` 를 부른다 → `out/<영상이름>/look.md`.
- 새 후보가 없으면 바로 3단계로. **새 후보가 있으면 선생님께 묻고**, 답을 look.md 에 적는다. 값이 문서 자체를 바꾸는 것이면(예: 새 개념 색) 해당 docs 를 고칠지 따로 묻는다.

## 3. 장면표 ✋ (director)
- `director` 를 부른다 → `out/<영상이름>/scenes.md`.
- 선생님께 보여 줄 것: 장면 표(번호 · 목적 · 화면 글 · 부품 · 길이) · 전체 길이 · 새 후보 · "줄임 — 확인 필요" 표시.
- 내레이션을 넣는 영상이면 `out/<영상이름>/narration.md` 대본도 같이 만들어 보여 준다 (`docs/video.md` 7장). 승인 뒤 메인이 ElevenLabs 로 소리 파일을 바로 만들어 `out/<영상이름>/audio/` 에 두고, director 가 **실제 소리 길이로 장면표를 다시 셈해서** 확정한다 — 어림 길이로 확정하지 않는다 (선생님 결정 2026-11-15, 7-1-robot-basics). 7-1 에서는 어림 2:43 이 실제 3:10 이 됐다.
- 장면표에 장면마다 **말하는 동안 움직일 대상**(`docs/motion.md` 6장)도 같이 적는다 (선생님 결정 2026-11-15, 7-1-robot-basics).
- ✋ 승인을 받으면 scenes.md 맨 위에 `승인: <날짜>` 를 적는다.

## 4. 스냅보드 ✋ (builder → critic)
- `builder` 를 부른다 → 장면마다 다 그린 마지막 모습 한 장 `out/<영상이름>/snapboard/<번호>.png`.
- `critic` 을 부른다 → `review-snapboard.md`. FAIL 이면 builder 가 FAIL 항목만 고치고 critic 이 다시 본다.
- critic PASS 뒤 선생님께 스냅보드 그림을 보여 준다 (그림 파일로 보내기). ✋

## 5. 생성 · 검수 (builder ↔ critic)
- `builder` 가 HyperFrames 프로젝트를 만든다 (`out/<영상이름>/video/`). 움직임은 motion.md 값 그대로.
- `critic` 이 판정한다 → `review.md`.
- FAIL → builder 가 FAIL 항목만 고침 → critic 다시. **3번 넘게 FAIL** 이거나 "판정 못 함"이 있으면 멈추고 선생님께 묻는다.
- 새 후보가 생기면 그때마다 멈추고 묻는다.

## 6. 렌더 (builder)
- critic PASS 뒤 `npx hyperframes preview --background` 로 미리보기 주소를 선생님께 준다. 선생님이 보고 OK 하면 렌더한다.
- `npx hyperframes render --quality delivery -o ../<영상이름>.mp4` (`out/<영상이름>/video/` 에서 실행 → `out/<영상이름>/<영상이름>.mp4`) → ffprobe 로 길이가 장면표와 같은지 확인.
- 선생님께 mp4 경로와 길이를 알려 준다.

## 7. 규칙 남기기 (메인)
- 이번 영상에서 선생님이 고치라고 한 것 · 새 후보로 정한 것을 모아 **다음 영상에도 쓸 규칙** 후보로 정리한다 (한 줄씩, 어디서 나왔는지).
- 선생님께 어느 것을 남길지 묻는다.
  - 값이 바뀌는 것(색 · 시간 · 크기) → 해당 `docs/*.md` 를 고친다 (출처: "선생님 결정 <날짜>, <영상이름>").
  - 일하는 방식 · 판단 기준 → `CLAUDE.md` "쌓인 규칙" 에 날짜와 함께 한 줄.
- `out/<영상이름>/notes.md` 에 이번 영상의 결정 · 질문 · 답을 남긴다.

## 어디서든 지킬 것
- 하위 담당(에이전트)은 선생님께 직접 묻지 못한다. 담당이 돌려준 "질문 · 새 후보"는 메인이 모아서 선생님께 한 번에 묻는다.
- 고정 파일(`docs/design.md` · `docs/motion.md` · `docs/video.md` · `src/parts/` · `src/assets/fonts/` · `docs/textbook/`)은 선생님 승인 없이 고치지 않는다.
- critic 은 판정만 한다. 고치는 것은 builder.
