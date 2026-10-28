# AMP RNote — Claude Code 작업 규칙

## 프로젝트
- 정부기준 전자연구노트 시스템 (㈜에이엠피시스템 연구전담부서)
- 명세(최우선): `docs/SPEC.html` — 개발 기술문서 RNOTE-SPEC-001 v1.0
- 화면: `docs/SCREENS.html` — 화면구성안 v1.0 (SC-01~SC-11, 브라우저로 열어 상단 탭으로 화면 전환)
- 스택: Next.js 14 App Router, TypeScript strict, Prisma, PostgreSQL 16

## 절대 규칙 (위반 시 작업 중단 후 보고)
1. NoteRevision / AuditLog / HashAnchor 에 update/delete 코드 금지 (append-only)
2. 모든 시각은 서버 DB now() — 클라이언트 시각을 저장하지 말 것
3. 해시 계산은 src/lib/hash.ts canonicalJSON만 사용, 필드 추가 시 hashVersion 올리고 DECISIONS.md 기록
4. AI 생성 텍스트는 본문과 분리(AiEvaluation) — 본문 반영은 기록자 사실확인 체크 후만
5. 노트 제출은 필수필드 + fileRefs ≥ 1 검증 통과 시에만
6. 모르는 설정값은 TODO_CONFIRM, 지어내지 말 것
7. 외부 발송(메일·카톡)은 NOTIFY_DRY_RUN=true 기본, 테스트에서 실발송 금지

## 작업 방식
- docs/SPEC.html 18장 Day 단위로 진행, 끝나면 19장 해당 T-xx 시험 작성·통과
- 화면 구현은 docs/SCREENS.html의 SC-xx 레이아웃·항목을 기준으로 한다
- 매 Day 종료: docs/PROGRESS.md 갱신 → 커밋 메시지 "D{n}: 요약"
- 커밋 후 `git rnp`(scripts/rn-push.sh)로 푸시 — 이 저장소도 연구노트 대상
- 변경한 md 문서 경로는 커밋 메시지 본문에 나열
- FMEA 표기는 "AIAG-VDA FMEA 1판"

## 명령
- npm run dev / npm run test / npm run verify:chain / npm run worker
- docker compose up -d db
