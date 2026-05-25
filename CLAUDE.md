# agentk — 구조 설계 에이전트 시스템

이 프로젝트는 소프트웨어 아키텍처 설계를 단계별로 수행하는 **agentk** 에이전트 시스템입니다.  
슬래시 커맨드(`/agentk/...`)로 각 단계의 에이전트를 호출하여 설계 활동을 진행합니다.

## 핵심 원칙

- **최적 설계**: 단일 품질이 아닌 전체 품질 균형을 고려한 설계 결정
- **활동 집중**: 각 에이전트는 자신의 책임 범위에만 집중하고, 다른 활동은 해당 에이전트에게 위임
- **단계별 수행**: 응답 길이 제한 회피를 위해 복잡한 작업은 반드시 단계별로 분할
- **Mermaid 다이어그램**: 모든 다이어그램은 Mermaid 문법 사용 (`graph TD`, `sequenceDiagram` 등)
- **ID 형식 준수**: UC-001, QS-001, CA-001, AD-001, NFR-001, QA-001 형식 사용

## 작업 디렉토리 규칙

- **설계 산출물**: `.vscode/settings.json`의 `agentk.architectureDirectory` 값 → 없으면 `docs`
- **소스 코드**: `.vscode/settings.json`의 `agentk.sourceDirectory` 값 → 없으면 `src`
- 작업 전 반드시 `.vscode/settings.json` 확인 후 디렉토리 결정

## 8-Phase 워크플로우

```
Phase 1: 시스템 정의      → /agentk/define-system, /agentk/analyze-business
Phase 2: 기능 명세        → /agentk/extract-usecases, /agentk/specify-usecase
Phase 3: 도메인 모델 정립 → /agentk/design-domain
Phase 4: 품질 요구사항 선정 → /agentk/elicit-scenarios, /agentk/specify-scenario,
                              /agentk/evaluate-scenarios, /agentk/select-scenarios
Phase 5: 후보 구조 설계   → /agentk/design-performance, /agentk/design-modifiability,
                              /agentk/design-msa, /agentk/design-packages,
                              /agentk/select-frameworks, /agentk/select-solutions
Phase 6: 최종 구조 설계   → /agentk/evaluate-candidates,
                              /agentk/integrate-deployment, /agentk/integrate-module
Phase 7: 구조 명세        → /agentk/specify-architecture
Phase 8: 구조 평가        → /agentk/analyze-architecture, /agentk/evaluate-architecture
```

## 산출물 디렉토리 구조 (기본: `docs/`)

```
docs/
├── system.md              # Phase 1: 시스템 정의
├── business.md            # Phase 1: 비즈니스 요구사항
├── usecases.md            # Phase 2: Use Case 목록
├── qualities.md           # Phase 4: 선정된 품질 요구사항
├── architecture.md        # Phase 7: 최종 구조 설계서
├── usecase/               # Phase 2: UC-nnn 상세 명세
├── domain/                # Phase 3: 도메인 모델 (model.md, UC-nnn.md)
├── quality/               # Phase 4: 품질 시나리오 (scenarios.md, QS-nnn.md, evaluations.md)
├── candidate/             # Phase 5: 후보 구조 (candidates.md, 관심사별 파일)
├── decision/              # Phase 6: 설계 결정 (decisions.md, evaluations.md)
├── architecture/          # Phase 6: 최종 구조 (deployment.md, module.md)
└── evaluation/            # Phase 8: 구조 평가 (decisions.md, evaluation.md)
```

## 품질 요구사항 유형

| 유형 | 이름 | 특징 |
|------|------|------|
| NFR | 비기능적 요구사항 | 허용치 미달 시 과제 실패, 명확한 측정값 필요 |
| QA | 품질 속성 | 더 많이 만족할수록 좋음, 우선순위 중요 |

## 상세 규칙 참조

- 공통 원칙: `.cursor/rules/agentk/foundation.md`
- 용어 정의: `.cursor/rules/agentk/glossary.md`
- 워크플로우: `.cursor/rules/agentk/workflow.md`
- 후보 구조 설계 기반: `.cursor/rules/agentk/candidate-architect.md`
- MSA 정의: `.cursor/rules/agentk/msa.md`
- 구조 명세 템플릿: `.cursor/rules/agentk/architecture-template.md`
