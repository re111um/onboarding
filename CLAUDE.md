# 피처링(Featuring Corp.) 신규입사자 온보딩

## 프로젝트 개요

신규입사자 또는 기존 직원이 Claude Code를 설치하고 커맨드를 실행하면,
AI가 가이드하는 인터랙티브 온보딩이 시작된다.

- **대상 A**: 피처링 신규입사자 전원 → `/onboarding`
- **대상 B**: 피처링 기존 직원 (Claude Code 도입) → `/cc-onboarding`
- **진행자**: HR (Thomas, U099RMP705B)
- **문서 인프라**: Atlassian MCP (Confluence 스페이스: FC)

---

## 트랙 구조

### 트랙 A — 신규입사자 온보딩 (`/onboarding`)

```
Step 0 → Step 1 → Step 2 → Step 3 → Step 4(보류) → Step 5 → Step 6(보류)
```

| Step | 이름 | 목표 | 산출물 |
|------|------|------|--------|
| Step 0 | 환경 설정 | Claude Code + Atlassian MCP 연결 | - |
| Step 1 | General | 컬쳐, 도구 세팅, Slack 인사 | 체크리스트 |
| Step 2 | Product | 피처링 플랫폼 이해 | 체험 리포트 |
| Step 3 | Biz | BM + 본부별 시나리오 퀘스트 | Biz 리포트 |
| Step 4 | Build Skill | _(구조만 존재, 내용 보류)_ | _(추후 고도화)_ |
| Step 5 | Wrap Up | 회고 + VoC + 킥오프 조언 | - |
| Step 6 | 플랫폼 체험 | 피처링 AI 솔루션 실습 | _(개발팀 협업 후)_ |

### 트랙 B — 기존직원 Claude Code 온보딩 (`/cc-onboarding`)

```
Phase 1(필수) → Phase 2(필수) → Phase 3(선택, 중간 하차 가능)
```

| Phase | 이름 | 목표 |
|-------|------|------|
| Phase 1 | 설치 + 기초 활용 | Claude Code 설치, 기본 커맨드, 핵심 프롬프트 패턴 |
| Phase 2 | 본부별 실무 활용 | 내 직무에 맞는 Claude 활용 시나리오 체험 |
| Phase 3 | 스킬 제작 (선택) | 스킬 해부 + 나만의 스킬 설계 (PR 보류) |

---

## 파일 구조

```
.claude/
  commands/
    onboarding.md          # /onboarding 진입점 (신규입사자 트랙)
    cc-onboarding.md       # /cc-onboarding 진입점 (기존직원 트랙)
  agents/
    onboarding-agent.md    # 신규입사자 트랙 에이전트
    cc-onboarding-agent.md # 기존직원 트랙 에이전트
  skills/
    step0-setup/           # 환경 설정 (공통 기반)
    step1-general/         # 컬쳐, 도구, Slack 인사
    step2-product/         # 피처링 플랫폼 이해
    step3-biz/             # BM + 본부별 시나리오
    step4-skill/           # 스킬 만들기 (보류 — 구조만)
    step5-wrapup/          # 회고 + 킥오프 조언
    step6-platform/        # 피처링 AI 솔루션 체험 (보류 — 개발팀 협업 후)
    cc-phase1-install/     # 기존직원: 설치 + 기초
    cc-phase2-practice/    # 기존직원: 본부별 실무 실습
    cc-phase3-skill/       # 기존직원: 스킬 제작 (선택)
config/
  confluence-ids.json      # Confluence 페이지 ID 매핑
  team-leads.json          # 조직 구조 및 온보딩 담당자
templates/                 # 산출물 템플릿
```

---

## STOP PROTOCOL

모든 스킬은 STOP PROTOCOL을 따른다.

### 각 Phase는 반드시 2턴에 걸쳐 진행

```
Phase A (첫 번째 턴):
1. references/에서 해당 Phase EXPLAIN 섹션 읽기
2. 내용 설명
3. references/에서 해당 Phase EXECUTE 섹션 읽기
4. "지금 직접 실행해보세요" 안내
5. 반드시 STOP. 턴 종료.

(입사자/직원이 "했어", "완료", "다음" 등을 입력)

Phase B (두 번째 턴):
1. references/에서 해당 Phase CHECK 섹션 읽기
2. AskUserQuestion으로 완료 확인
3. 피드백 + 격려
4. 다음 Phase로 이동할지 묻기
```

### 핵심 금지 사항
- Phase A에서 AskUserQuestion 호출 금지
- Phase A에서 CHECK 먼저 진행 금지
- 한 턴에 EXPLAIN + CHECK 동시 진행 금지

---

## MCP 연결 전제 조건

### Atlassian MCP
- Step 0에서 Atlassian MCP 연결 완료를 전제로 한다
- 연결 실패 시: "Atlassian 커넥터 연결이 아직 안 된 것 같아요" 안내 후
  Claude.ai > Settings > Integrations에서 Atlassian 연결 방법 재안내
- 회사 계정(`@featuring.in`)으로 OAuth 인증했는지 확인
- MCP 실패로 온보딩 전체가 멈추면 안 됨 — 해당 실습 스킵 후 다음으로 진행

### Slack MCP
- 완료 알림 DM 및 커피챗 연결에 사용
- 실패 시 수동 안내로 대체

### Confluence 동적 참조
- `config/confluence-ids.json`의 페이지 ID로 Atlassian MCP를 통해 최신 콘텐츠를 fetch한다
- 하드코딩하지 않는다
- 스페이스 키: `FC` / 베이스 URL: `https://featuring-corp.atlassian.net`

---

## 조직 구조 (2025 Q1 기준)

4개 본부 구조. 2분기 개편 예정이나 본부는 유지됨.

```
피처링
├── 경영관리본부 (Elly / CFO)
│   └── 경영인프라팀 (Raine)
├── 프로덕트본부 (Poza / CTO)
│   ├── CDO스쿼드 (Ray 임시)
│   ├── 콘텐츠관리스쿼드 (Tina)
│   ├── 엔진팀 (Earl)
│   └── 디자인팀 (Ray)
├── 세일즈&마케팅본부 (Martin / 대표 겸)
│   ├── 마케팅팀 (Eve)
│   └── 본부직속 (Eve 담당)
└── 인플루언서비즈니스본부 (Elly / CFO 겸)
    ├── 캠페인팀 (Gina)
    └── 커머스팀 (Nana)
```

---

## Step 3 본부별 시나리오 배정

| 본부 | 시나리오 관점 | 파일 |
|------|-------------|------|
| 경영관리본부 | HR/재무/법무/운영 | `phase2-scenarios-mgmt.md` |
| 프로덕트본부 | SaaS 개발/PM/디자인 | `phase2-scenarios-product.md` |
| 세일즈&마케팅본부 | B2B 세일즈 + 퍼포먼스 마케팅 | `phase2-scenarios-sales.md` |
| 인플루언서비즈니스본부 | 캠페인 기획/운영 + 커머스 | `phase2-scenarios-influencer.md` |

---

## 산출물 저장

- 원본: Confluence 페이지 (Atlassian MCP로 저장)
- Fallback: `outputs/{닉네임}-{입사일}/` (MCP 실패 시)

---

## 프로젝트 문서 (Lazy Loading)

필요할 때만 읽는다:
- 조직 구조 및 담당자: @config/team-leads.json
- Confluence 페이지 ID: @config/confluence-ids.json

---

## 언어 및 톤

- 모든 응답은 한국어로 작성
- 닉네임으로 호칭 (존칭 없이 닉네임만 — 예: "Thomas", "Earl")
- 친근하고 환영하는 톤 유지
- 존댓말 사용
