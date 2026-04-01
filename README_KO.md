<p align="center">
  <h1 align="center">OpenCode Game Studios</h1>
  <p align="center">
    OpenCode 세션 하나로 완전한 게임 개발 스튜디오를 구성하세요.
    <br />
    48개 에이전트. 37개 워크플로우. 하나의 조율된 AI 팀.
  </p>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT License"></a>
  <a href=".opencode/agents"><img src="https://img.shields.io/badge/agents-48-blueviolet" alt="48 Agents"></a>
  <a href=".opencode/skills"><img src="https://img.shields.io/badge/skills-37-green" alt="37 Skills"></a>
  <a href=".opencode/scripts"><img src="https://img.shields.io/badge/scripts-8-orange" alt="8 Scripts"></a>
  <a href=".opencode/rules"><img src="https://img.shields.io/badge/rules-11-red" alt="11 Rules"></a>
  <a href="https://opencode.ai"><img src="https://img.shields.io/badge/built%20for-OpenCode-f5f5f5" alt="Built for OpenCode"></a>
</p>

<p align="center">
  <a href="README.md">English</a>
</p>

---

> **[Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios)**(by Donchitos)에서 마이그레이션된 프로젝트입니다.
> 오픈소스 AI 코딩 도구인 [OpenCode](https://github.com/anomalyco/opencode)에서 동작하도록 비공식 포팅한 버전입니다.
> 에이전트 아키텍처, 프롬프트, 워크플로우의 원작자는 Donchitos입니다.

---

## 왜 이게 필요한가

AI와 함께 혼자 게임을 만드는 건 강력한 방법이지만 — 단순한 채팅 세션에는 구조가 없습니다. 마법 숫자를 하드코딩하거나, 설계 문서를 건너뛰거나, 스파게티 코드를 작성해도 아무도 막지 않습니다. QA 검토도 없고, 디자인 리뷰도 없고, "이게 게임 비전에 맞는가?"라고 묻는 사람도 없습니다.

**OpenCode Game Studios**는 AI 세션에 실제 스튜디오의 구조를 부여해 이 문제를 해결합니다. 범용 어시스턴트 하나 대신, 스튜디오 계층으로 조직된 48개의 전문 에이전트를 갖게 됩니다. 비전을 지키는 디렉터, 각 도메인을 소유한 부서 리드, 실제 작업을 수행하는 스페셜리스트로 구성됩니다.

결과적으로: 모든 결정은 여전히 당신이 내리지만, 이제 올바른 질문을 던지고, 실수를 일찍 잡아내고, 첫 브레인스토밍부터 출시까지 프로젝트를 체계적으로 유지하는 팀이 생깁니다.

---

## 목차

- [포함된 것들](#포함된-것들)
- [스튜디오 계층](#스튜디오-계층)
- [슬래시 커맨드](#슬래시-커맨드)
- [시작하기](#시작하기)
- [모델 설정](#모델-설정)
- [프로젝트 구조](#프로젝트-구조)
- [작동 방식](#작동-방식)
- [설계 철학](#설계-철학)
- [커스터마이징](#커스터마이징)
- [원본과의 차이점](#원본과의-차이점)
- [라이선스](#라이선스)

---

## 포함된 것들

| 카테고리 | 수량 | 설명 |
|----------|------|------|
| **에이전트** | 48 | 디자인, 프로그래밍, 아트, 오디오, 내러티브, QA, 프로덕션 전문 서브에이전트 |
| **스킬** | 37 | 일반 워크플로우를 위한 슬래시 커맨드 (`/start`, `/sprint-plan`, `/code-review`, `/brainstorm` 등) |
| **스크립트** | 8 | 커밋, 푸시, 에셋 변경, 세션 수명주기 등 자동 검증 유틸리티 |
| **규칙** | 11 | 게임플레이, 엔진, AI, UI, 네트워크 코드 편집 시 적용되는 경로 기반 코딩 표준 |
| **템플릿** | 29 | GDD, ADR, 스프린트 플랜, 경제 모델, 팩션 설계 등 문서 템플릿 |

## 스튜디오 계층

에이전트는 실제 스튜디오 운영 방식과 동일하게 3단계로 조직됩니다:

```
Tier 1 — 디렉터 (PRIMARY_MODEL)
  creative-director    technical-director    producer

Tier 2 — 부서 리드 (STANDARD_MODEL)
  game-designer        lead-programmer       art-director
  audio-director       narrative-director    qa-lead
  release-manager      localization-lead

Tier 3 — 스페셜리스트 (STANDARD_MODEL / FAST_MODEL)
  gameplay-programmer  engine-programmer     ai-programmer
  network-programmer   tools-programmer      ui-programmer
  systems-designer     level-designer        economy-designer
  technical-artist     sound-designer        writer
  world-builder        ux-designer           prototyper
  performance-analyst  devops-engineer       analytics-engineer
  security-engineer    qa-tester             accessibility-specialist
  live-ops-designer    community-manager
```

### 엔진 스페셜리스트

세 가지 주요 엔진에 대한 에이전트 세트가 포함되어 있습니다:

| 엔진 | 리드 에이전트 | 서브 스페셜리스트 |
|------|-------------|-----------------|
| **Godot 4** | `godot-specialist` | GDScript, Shaders, GDExtension |
| **Unity** | `unity-specialist` | DOTS/ECS, Shaders/VFX, Addressables, UI Toolkit |
| **Unreal Engine 5** | `unreal-specialist` | GAS, Blueprints, Replication, UMG/CommonUI |

## 슬래시 커맨드

OpenCode에서 `/`를 입력하면 37개의 스킬에 접근할 수 있습니다:

**리뷰 & 분석**
`/design-review` `/code-review` `/balance-check` `/asset-audit` `/scope-check` `/perf-profile` `/tech-debt`

**프로덕션**
`/sprint-plan` `/milestone-review` `/estimate` `/retrospective` `/bug-report`

**프로젝트 관리**
`/start` `/project-stage-detect` `/reverse-document` `/gate-check` `/map-systems` `/design-system`

**릴리즈**
`/release-checklist` `/launch-checklist` `/changelog` `/patch-notes` `/hotfix`

**크리에이티브**
`/brainstorm` `/playtest-report` `/prototype` `/onboard` `/localize`

**팀 오케스트레이션** (하나의 기능에 여러 에이전트 동시 투입)
`/team-combat` `/team-narrative` `/team-ui` `/team-release` `/team-polish` `/team-audio` `/team-level`

## 시작하기

### 사전 준비

- [Git](https://git-scm.com/)
- [OpenCode](https://opencode.ai) (`npm install -g opencode`)
- **권장**: [jq](https://jqlang.github.io/jq/), Python 3 (JSON 검증용)

### 설치

1. **클론 또는 템플릿으로 사용**:
   ```bash
   git clone https://github.com/YOUR-ORG/OpenCode-Game-Studios.git my-game
   cd my-game
   ```

2. **Git 훅 활성화**:
   ```bash
   git config core.hooksPath .githooks
   ```

3. **모델 설정** — `opencode.json`에서 플레이스홀더를 실제 모델로 교체:
   ```json
   "model": "openai/gpt-4o",
   "small_model": "openai/gpt-4o-mini"
   ```
   에이전트 파일의 `${STANDARD_MODEL}`, `${FAST_MODEL}`도 교체하거나, `opencode.json`의 `model`을 기본값으로 설정하면 에이전트가 상속합니다.

4. **OpenCode 시작**:
   ```bash
   opencode
   ```

5. **`/start` 실행** — 현재 상태를 묻고 맞는 워크플로우로 안내합니다. 가정 없이 시작합니다.

   또는 이미 무엇이 필요한지 안다면 바로 스킬로:
   - `/brainstorm` — 게임 아이디어를 처음부터 탐색
   - `/setup-engine godot 4.6` — 엔진 설정
   - `/project-stage-detect` — 기존 프로젝트 분석

## 모델 설정

이 프로젝트는 특정 AI 제공자에 종속되지 않습니다. `opencode.json`에서 원하는 모델을 설정하세요:

| 플레이스홀더 | 용도 | 예시 |
|-------------|------|------|
| `${PRIMARY_MODEL}` | Tier 1 디렉터 (가장 강력한 모델 권장) | `openai/gpt-4o`, `anthropic/claude-sonnet-4-20250514`, `google/gemini-2.5-pro` |
| `${STANDARD_MODEL}` | Tier 2 리드 & Tier 3 스페셜리스트 | `openai/gpt-4o`, `anthropic/claude-sonnet-4-20250514` |
| `${FAST_MODEL}` | 타이틀 생성 등 경량 작업 | `openai/gpt-4o-mini`, `anthropic/claude-haiku-4-5` |

OpenCode는 75개 이상의 프로바이더를 지원합니다. [opencode.ai/docs](https://opencode.ai/docs)에서 전체 목록을 확인하세요.

## 프로젝트 구조

```
AGENTS.md                           # 프로젝트 인스트럭션 (OpenCode가 자동으로 읽음)
opencode.json                       # 권한, 모델 설정, MCP 서버
.opencode/
  agents/                           # 48개 에이전트 정의 (마크다운 + YAML 프론트매터)
  skills/                           # 37개 슬래시 커맨드 (스킬별 서브디렉토리)
  rules/                            # 11개 경로 기반 코딩 표준
  scripts/                          # 8개 유틸리티 스크립트 (검증, 세션 상태)
  commands/                         # 5개 커스텀 /커맨드
  docs/
    quick-start.md                  # 상세 사용 가이드
    agent-roster.md                 # 전체 에이전트 목록
    agent-coordination-map.md       # 위임 및 에스컬레이션 경로
    templates/                      # 29개 문서 템플릿
.githooks/                          # pre-commit, pre-push 검증 훅
src/                                # 게임 소스 코드
assets/                             # 아트, 오디오, VFX, 셰이더, 데이터 파일
design/                             # GDD, 내러티브 문서, 레벨 디자인
docs/                               # 기술 문서 및 ADR
tests/                              # 테스트 스위트
prototypes/                         # 임시 프로토타입 (src/와 격리)
production/                         # 스프린트 플랜, 마일스톤, 릴리즈 추적
```

## 작동 방식

### 에이전트 조율

에이전트는 구조화된 위임 모델을 따릅니다:

1. **수직 위임** — 디렉터 → 리드 → 스페셜리스트로 위임
2. **수평 협의** — 같은 티어 에이전트끼리 협의 가능하나 도메인 외 결정 불가
3. **충돌 해결** — 이견은 공통 상위 에이전트으로 에스컬레이션 (디자인→`creative-director`, 기술→`technical-director`)
4. **변경 전파** — 부서 간 변경은 `producer`가 조율
5. **도메인 경계** — 명시적 위임 없이 자기 도메인 외 파일 수정 불가

### 협업형, 자율형이 아님

이것은 **자동 실행** 시스템이 아닙니다. 모든 에이전트는 엄격한 협업 프로토콜을 따릅니다:

1. **먼저 물어보기** — 해결책 제안 전에 질문
2. **옵션 제시** — 장단점과 함께 2-4개 선택지 제시
3. **당신이 결정** — 최종 판단은 항상 사용자
4. **초안 공유** — 확정 전에 작업물 공유
5. **승인 후 작성** — 동의 없이는 파일 수정 없음

### 검증 스크립트

`.opencode/scripts/`의 스크립트들을 수동으로 실행하거나 커스텀 커맨드로 호출할 수 있습니다:

| 스크립트 | 커맨드 | 기능 |
|----------|--------|------|
| `validate-commit.sh` | — | 하드코딩 값, JSON 유효성, 설계 문서 섹션 검사 |
| `validate-push.sh` | — | 보호 브랜치 푸시 경고 |
| `validate-assets.sh` | `/validate-assets` | 에셋 네이밍 규칙 및 JSON 구조 검증 |
| `session-start.sh` | `/session-context` | 스프린트 컨텍스트 및 최근 git 활동 로드 |
| `detect-gaps.sh` | `/detect-gaps` | 문서 누락, 프로토타입 미문서화 감지 |
| `pre-compact.sh` | `/save-state` | 컨텍스트 압축 전 세션 상태 저장 |
| `session-stop.sh` | `/session-end` | 세션 요약 로그 |

**Git 훅**은 `.githooks/`에서 `pre-commit`(커밋 검증)과 `pre-push`(보호 브랜치 경고)를 제공합니다.

### 경로 기반 규칙

파일 위치에 따라 코딩 표준이 자동 적용됩니다:

| 경로 | 적용 규칙 |
|------|-----------|
| `src/gameplay/**` | 데이터 기반 값, 델타 타임, UI 참조 금지 |
| `src/core/**` | 핫패스 제로 할당, 스레드 안전, API 안정성 |
| `src/ai/**` | 성능 예산, 디버깅 가능성, 데이터 기반 파라미터 |
| `src/networking/**` | 서버 권위적, 버전된 메시지, 보안 |
| `src/ui/**` | 게임 상태 소유 금지, 로컬라이제이션 대응, 접근성 |
| `design/gdd/**` | 필수 8개 섹션, 공식 형식, 엣지 케이스 |
| `tests/**` | 테스트 네이밍, 커버리지 요구사항, 픽스처 패턴 |
| `prototypes/**` | 완화된 표준, README 필수, 가설 문서화 |

## 설계 철학

이 템플릿은 전문적인 게임 개발 방법론을 기반으로 합니다:

- **MDA 프레임워크** — 게임 디자인을 위한 메카닉스, 다이나믹스, 에스테틱스 분석
- **자기결정이론** — 플레이어 동기 부여를 위한 자율성, 유능감, 관계성
- **플로우 스테이트 디자인** — 플레이어 몰입을 위한 도전-스킬 균형
- **바틀 플레이어 유형** — 타겟 오디언스 설정 및 검증
- **검증 주도 개발** — 구현 전 테스트 작성

## 커스터마이징

이것은 **템플릿**이지, 고정된 프레임워크가 아닙니다. 모든 것을 커스터마이즈할 수 있습니다:

- **에이전트 추가/제거** — 불필요한 에이전트 파일 삭제, 새 도메인용 에이전트 추가
- **에이전트 프롬프트 수정** — 에이전트 행동 조정, 프로젝트별 지식 추가
- **스킬 수정** — 팀 프로세스에 맞게 워크플로우 조정
- **규칙 추가** — 프로젝트 디렉토리 구조에 맞는 새 경로 규칙 생성
- **엔진 선택** — Godot, Unity, Unreal 에이전트 세트 중 선택 (또는 모두 유지)

## 원본과의 차이점

| 항목 | 원본 (Claude Code Game Studios) | 이 프로젝트 (OpenCode 포트) |
|------|--------------------------------|---------------------------|
| **도구** | Claude Code (Anthropic 전용) | OpenCode (75개+ 프로바이더 지원) |
| **설정 파일** | `CLAUDE.md` + `.claude/settings.json` | `AGENTS.md` + `opencode.json` |
| **에이전트 디렉토리** | `.claude/agents/` | `.opencode/agents/` |
| **훅 시스템** | Claude Code 내장 훅 (SessionStart 등) | git hooks + 유틸리티 스크립트 |
| **모델** | Anthropic Claude (opus/sonnet/haiku) | 프로바이더 자유롭게 선택 |
| **라이선스** | MIT | MIT |

원본 프로젝트의 모든 기능(48 에이전트, 37 스킬, 11 규칙, 29 템플릿)이 그대로 포팅되어 있습니다.

## 라이선스

MIT License. 자세한 내용은 [LICENSE](LICENSE)를 참조하세요.
