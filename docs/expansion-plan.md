# Harness Codex 확장 계획안

작성일: 2026-05-21
현재 버전: 0.1.0

## 요약

`harness-codex` 는 현재 v0.1 (Installable Guided Skill) 단계로, 원본 `revfactory/harness` 의 사상 일부만 포팅된 MVP 상태이다. 본 계획안은 공식 로드맵(`docs/roadmap.md`)의 breadth 방향(도메인 템플릿/자동화 레시피/마이그레이션)과 별개로, **depth 방향의 갭 — "진화하는 시스템" 정체성** — 을 우선 채우는 순서를 제안한다.

핵심 권고: **v0.2를 depth 우선으로 잡고 (Phase 0 audit + 변경 이력 + Phase 7 진화 루프), 그 다음 Progressive Disclosure 구조를 도입한 뒤, 그 위에서 도메인 템플릿과 6패턴 선택을 쌓는다.**

---

## 1. 현재 상태 (v0.1)

### 산출물
- `plugins/harness-codex/.codex-plugin/plugin.json` (v0.1.0)
- `plugins/harness-codex/skills/harness/SKILL.md` (151줄)
- `.agents/plugins/marketplace.json`
- `docs/architecture.md`, `docs/installation.md`, `docs/migration-from-claude-harness.md`, `docs/roadmap.md`
- `README.md`, `harness-codex-overview.md`

### v0.1 SKILL.md에 이미 포함된 것
- 7단계 default workflow
- Repository inspection checklist
- Harness plan format
- Generated skill 가이드라인
- AGENTS.md 가이드라인
- Claude Harness 마이그레이션 가이드 (간략)
- KO/EN invocation 예시
- Output style

### v0.1을 점진 설계한 합리적 이유 (회고)
1. Codex 플러그인 시스템 자체의 작동 검증이 선행 필요 — 마켓플레이스 add, install, skill 트리거가 실제로 도는지
2. 사용자 피드백 없는 상태에서 도메인 템플릿은 추측 — 실제 사용 패턴 관찰 후 만드는 게 정확함
3. 유지보수 부담 누적 회피 — 각 단계에서 정말 필요한지 검증
4. Codex의 subagent/team 프리미티브 미확인 — 원본 `TeamCreate + SendMessage + TaskCreate` 는 Claude Code 전용. Codex 동등물 확인 전에 multi-agent 박는 건 위험

이 결정은 유지한다. 단계적 확장의 근거다.

---

## 2. 원본 revfactory/harness 대비 갭 분석

### 공식 로드맵이 다루는 갭 (breadth)
- v0.2: 도메인별 템플릿 (frontend/backend/data/research)
- v0.3: 자동화 레시피 (daily/weekly checks)
- v0.4: Claude Harness 마이그레이션 본격화

### 공식 로드맵이 다루지 않는 갭 (depth)

| 갭 | 중요도 | 의존성 |
|---|---|---|
| Phase 0 audit (기존 산출물 감지 + drift + 분기) | Critical | 없음 |
| Progressive Disclosure (`SKILL.md` ≤500줄 + `references/` 조건부 로딩) | Critical | 다른 모든 확장의 구조적 기반 |
| 변경 이력 테이블 (`AGENTS.md` 또는 `CHANGELOG.md` 안에 표준화) | High | Phase 0 audit 필요 |
| Phase 7 진화 루프 (실행 후 피드백 → 수정 대상 매트릭스) | High | 변경 이력 필요 |
| 6 아키텍처 패턴 선택 (Pipeline/Fan-out/Producer-Reviewer/Supervisor/Hierarchical/Expert Pool) | Medium | Progressive Disclosure 필요 |
| Codex subagent 오케스트레이션 (Codex 동등물 조사 후) | Medium | Codex CLI subagent 기능 조사 선행 |
| 검증 단계 (with/without 비교, should/should-NOT 트리거 테스트) | Low | 다른 게 안정된 후 |

### 판단
- breadth 산출물은 사용자 프로젝트에 안 맞으면 버려진다 → 가변 가치
- depth 산출물은 모든 프로젝트에서 작동하는 기반 → 고정 가치

ROI 관점에서 **depth 우선 → breadth 추가** 순서가 합리적이다.

---

## 3. 제안 버전 시퀀스

### v0.2 — "진화하는 시스템" 정체성 완성

**목표:** 한 번 만들고 끝나는 정적 산출물이 아니라, 매 실행 후 자체 갱신되는 시스템으로 전환.

**범위:**
- Phase 0 audit 단계 추가 — 기존 `AGENTS.md`/`.agents/skills/`/`docs/harness/` 감지 → drift 보고 → 신규 구축/기존 확장/유지보수 분기 결정
- 변경 이력 표준화 — `AGENTS.md` 하단 또는 별도 `CHANGELOG.md` 에 `| 날짜 | 변경 내용 | 대상 | 사유 |` 4열 테이블 의무화
- Phase 7 진화 루프 추가 — 실행 완료 후 피드백 요청, 피드백 유형별 수정 대상 매트릭스, 진화 트리거 (반복 피드백 2회 이상 / 반복 실패 / 수동 우회 관찰)
- "기존 확장 시 Phase 선택 매트릭스" 명시 — 어떤 변경 유형이 어떤 Phase 재실행을 트리거하는지

**파일 변경:**
- `plugins/harness-codex/skills/harness/SKILL.md` — Phase 0 / Phase 7 / 변경 이력 섹션 추가 (현 151줄 → 약 250-300줄 예상)
- `plugins/harness-codex/.codex-plugin/plugin.json` — version `0.1.0` → `0.2.0`
- `docs/roadmap.md` — v0.2 항목 갱신
- `docs/architecture.md` — 진화 루프 반영
- `CHANGELOG.md` — 신설, 본 버전부터 시작
- `harness-codex-overview.md` — Phase 0/7 추가 반영

**완료 기준:**
- 기존 산출물이 있는 repo 에서 harness 재실행 시 신규 생성 아니라 audit → 확장 모드로 분기
- 모든 변경이 `CHANGELOG.md` 또는 `AGENTS.md` 변경 이력 표에 기록됨
- 실행 종료 시 사용자 피드백 요청 단계 명시

---

### v0.3 — Progressive Disclosure 구조 도입

**목표:** SKILL.md 비대화 방지 + 조건부 로딩 가능한 references/ 컨테이너 확보. 이후 확장(6패턴, 템플릿 등)의 구조적 기반.

**범위:**
- SKILL.md ≤500줄 룰 명시 — 초과 시 references/ 로 분리 의무
- `plugins/harness-codex/skills/harness/references/` 디렉토리 신설
- 기존 SKILL.md 의 일부 섹션을 references/ 로 분리:
  - `references/inspection-checklist.md` — repo inspection 체크리스트
  - `references/plan-format.md` — Harness plan 형식
  - `references/skill-writing-guide.md` — generated skill 가이드라인 (확장본)
  - `references/agents-md-guide.md` — AGENTS.md 작성 가이드
  - `references/claude-migration.md` — Claude harness 마이그레이션 가이드
- SKILL.md 본문에는 각 reference 로의 "언제 읽어라" 포인터만 남김
- references 파일 내부에서도 300줄 초과 시 ToC 의무화

**파일 변경:**
- `plugins/harness-codex/skills/harness/SKILL.md` — 본문 ≤500줄로 다이어트, references/ 포인터 추가
- `plugins/harness-codex/skills/harness/references/*.md` — 신규 파일 5개 (분리된 섹션)
- `plugins/harness-codex/.codex-plugin/plugin.json` — version `0.2.0` → `0.3.0`
- `docs/architecture.md` — Progressive Disclosure 패턴 설명

**완료 기준:**
- SKILL.md ≤500줄
- 모든 reference 파일이 명확한 단일 책임
- 각 reference 가 SKILL.md 의 어디서 참조되는지 명시

---

### v0.4 — AGENTS.md 템플릿 + 도메인별 예시 (공식 v0.2 흡수)

**목표:** 사용자 진입 장벽 낮추기. 처음 harness 쓸 때 즉시 활용 가능한 출발점 제공.

**범위:**
- `AGENTS.md` 표준 템플릿 (도메인 무관 공통 골격)
- 도메인별 변형 4종:
  - frontend (React/Next.js/Vue 등)
  - backend (Node/Python/Go 서버)
  - data (Jupyter/dbt/airflow)
  - research (notebooks + 실험 추적)
- 각 도메인별로 추천 skill 1-3개 예시 포함
- 검증 체크리스트

**파일 변경:**
- `plugins/harness-codex/skills/harness/references/templates/agents-md-base.md`
- `plugins/harness-codex/skills/harness/references/templates/frontend.md`
- `plugins/harness-codex/skills/harness/references/templates/backend.md`
- `plugins/harness-codex/skills/harness/references/templates/data.md`
- `plugins/harness-codex/skills/harness/references/templates/research.md`
- `plugins/harness-codex/skills/harness/references/validation-checklist.md`
- SKILL.md — Phase 1 도메인 감지 결과에 따라 templates/ 로 분기하는 포인터 추가
- version → `0.4.0`

**완료 기준:**
- 4개 도메인 각각 대해 harness 호출 시 적절한 템플릿이 제안됨
- 템플릿이 그대로 적용 가능 (placeholder 형태로 작성)

---

### v0.5 — 6 패턴 선택 + Codex subagent 오케스트레이션 조사

**목표:** 도메인에 따른 아키텍처 패턴 자동 선택. 원본 harness 의 핵심 차별화 기능.

**범위:**
- **선행 조사 필수:** Codex CLI 가 subagent 호출, 백그라운드 실행, agent 간 통신을 어디까지 지원하는지 문서화. 지원 안 되는 영역은 명시.
- 6 패턴 정의 (Pipeline / Fan-out·Fan-in / Producer-Reviewer / Supervisor / Hierarchical / Expert Pool)
- 도메인/작업 특성 → 패턴 매핑 가이드
- 각 패턴별 Codex 구현 예시 (Codex 가 지원하는 범위 내에서)
- 지원 안 되는 패턴은 "Codex 제약으로 인해 단순화 또는 미지원" 명시

**파일 변경:**
- `plugins/harness-codex/skills/harness/references/agent-design-patterns.md` (메인 결과물)
- `plugins/harness-codex/skills/harness/references/codex-subagent-capabilities.md` (조사 결과)
- SKILL.md — Phase 2 (팀 아키텍처 설계) 추가
- version → `0.5.0`

**완료 기준:**
- 사용자가 도메인 묘사 시 적절한 패턴 1개가 자동 추천됨
- Codex 제약이 명시적으로 문서화됨

---

### v0.6 — 자동화 레시피 (공식 v0.3) + 검증 단계

**목표:** 반복 가능한 자동화 + harness 산출물 자체의 품질 보증.

**범위:**
- 자동화 레시피 (daily/weekly checks, dependency review, test health)
- "자동화하지 말 것" 가이드 (안전 기준)
- with-skill vs without-skill 비교 테스트 방법론
- should-trigger / should-NOT-trigger 8-10 쿼리 검증
- 드라이런 테스트 (Phase 순서, 데이터 흐름, dead-link 확인)

**파일 변경:**
- `plugins/harness-codex/skills/harness/references/automation-recipes.md`
- `plugins/harness-codex/skills/harness/references/testing-guide.md`
- SKILL.md — Phase 6 (검증) 추가
- version → `0.6.0`

---

### v0.7 — Claude Harness 마이그레이션 정식화 (공식 v0.4)

**범위:**
- `.claude/agents/*` → Codex 등가물 변환 가이드 확장
- `.claude/skills/*` → `.agents/skills/*` 변환 매핑
- before/after 샘플
- Claude 전용 호출(`TeamCreate`, `SendMessage`) 의 Codex 대체 또는 미지원 명시
- HyperClass 같은 거버넌스 중심 프로젝트의 마이그레이션 케이스

**파일 변경:**
- `plugins/harness-codex/skills/harness/references/claude-migration.md` (확장)
- `docs/migration-from-claude-harness.md` (확장)
- `docs/examples/claude-to-codex/` (before/after 샘플)
- version → `0.7.0`

---

## 4. Open Questions

답을 정해야 진행 가능한 항목들:

1. **Codex CLI 의 plugin install 명령 정확한 형태 확인 필요** — `codex plugin marketplace add ...` 가 실제로 존재하는 명령인지, 마켓플레이스 메커니즘이 동작하는지. v0.1 의 README 가 가정하는 명령 체계가 실제와 일치하는지 검증.

2. **Codex subagent 프리미티브 범위** — Codex 가 background subagent, agent 간 메시지 전달, 공유 작업 목록 등을 어디까지 지원하는지. v0.5 의 6 패턴 구현 가능 범위를 결정함.

3. **`CHANGELOG.md` vs `AGENTS.md` 변경 이력 위치** — 원본 harness 는 CLAUDE.md 안에 변경 이력 테이블을 둠. Codex 에서는 AGENTS.md 안에 둘지, 별도 CHANGELOG.md 로 분리할지. 권고: AGENTS.md 안에 두는 게 원본 사상과 일관됨 (포인터 + 변경 이력 합쳐서).

4. **Progressive Disclosure 의 references/ 가 Codex 환경에서 실제로 조건부 로딩되는지** — Claude Code 는 description 매칭 기반 로딩이 작동하지만, Codex 의 skill 메커니즘이 references/ 폴더를 어떻게 다루는지 확인 필요. 조건부 로딩이 안 되면 SKILL.md 다이어트의 실효가 없음.

5. **공식 로드맵과의 정합성** — 본 계획안은 공식 `docs/roadmap.md` 의 순서 (v0.2 템플릿 / v0.3 자동화 / v0.4 마이그레이션) 와 다르다. 공식 로드맵을 갱신할지 (depth 우선으로 재정렬) 또는 두 트랙을 병행할지 결정 필요. 권고: 본 계획안 채택 시 `docs/roadmap.md` 도 갱신.

---

## 5. 진행 방식 권고

각 버전은 독립 PR/커밋으로 분리한다. 한 버전을 머지한 후 다음으로 진행. 이유:

- 각 버전이 그 자체로 동작 가능한 단위 (v0.2 머지 후 v0.3 안 해도 v0.2 가치 유효)
- 회귀 발생 시 어느 버전이 원인인지 명확
- 사용자 피드백을 각 버전마다 받을 수 있음 (Phase 7 사상과 일치)

각 버전 진입 전 체크:
- [ ] 직전 버전이 동작하는지 (수동 검증)
- [ ] Open Questions 중 해당 버전에 필요한 답이 확보되었는지
- [ ] `CHANGELOG.md` 갱신
- [ ] `plugin.json` 버전 bump
- [ ] `README.md`, `harness-codex-overview.md` 의 invocation 예시/스킬 설명 정합성

---

## 6. 본 계획안 자체에 대한 기록

본 문서는 작업 진입 전 합의용 계획안이다. 실제 진행 중 변경 사항은 본 문서를 갱신하거나 폐기 후 새 계획안으로 대체한다. 변경 결정은 `CHANGELOG.md` 에 기록.
