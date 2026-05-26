# QS-001-TTFT

## 개요

### Quality Scenario ID
QS-001

### 제목
TTFT (Time To First Token)

### 설명
추론 요청에 대해 첫 토큰이 생성되기까지의 시간. Tiered Memory 내 KV Cache 배치 결정(UC-004)의 핵심 목표 지표.

### 품질 속성
성능 (지연)

## 환경

### 시스템 상태
MCR Runtime이 LLM 서빙 프레임워크와 통합되어 정상 가동 중이며, KV Cache가 이기종 메모리 계층(PIM/PNM·DRAM·CXL·SSD)에 분산 배치되어 있다.

### 초기 조건
- 성능 Cost 모델이 구성·로드되어 있다.
- 각 메모리 계층의 상태·용량·비용 텔레메트리가 수집되어 있다.
- 대상 추론 요청의 컨텍스트(토큰 길이 등)가 주어진다.

### 부하 조건
일반 운영 부하 및 메모리 계층별 용량이 부분적으로 점유된 상태.

### 관련 컴포넌트
- KVCachePlacementPlanner
- SystemStateStore
- CostModelStore
- MemoryTierInterface
- ServingGatewayAPI

## 동작

서빙 프레임워크가 추론 요청을 전달하면, 시스템은 시스템 상태와 Cost 모델을 참조하여 KV Cache의 계층 배치를 결정하고, 결정된 배치에 따라 첫 토큰 생성을 위한 연산을 수행한다. 첫 토큰이 생성되어 서빙 프레임워크로 반환된다.

## 측정

- 측정 항목: TTFT (ms)
- 측정 공식:

```
TTFT = [첫 토큰 생성 완료 시각] - [추론 요청 도착 시각]
```

## 관련 문서

- UC-004 (KV Cache 계층 배치 결정)
- UC-001 (비용 인지 메모리 중심 추론 스케줄링)
- 컴포넌트: KVCachePlacementPlanner, MemoryTierInterface
