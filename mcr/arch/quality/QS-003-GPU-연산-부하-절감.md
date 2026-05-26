# QS-003-GPU-연산-부하-절감

## 개요

### Quality Scenario ID
QS-003

### 제목
GPU 연산 부하 절감

### 설명
Computable-Memory 오프로딩(UC-006/007)과 KV 재사용(UC-002) 적용 시 GPU 연산 부하가 Baseline 대비 절감되는 정도.

### 품질 속성
성능 (자원 효율)

## 환경

### 시스템 상태
Baseline(GPU 중심) 구성과 MCR Runtime(오프로딩·재사용 적용) 구성이 동일 워크로드에 대해 비교 가능한 상태로 준비되어 있다.

### 초기 조건
- 동일한 모델·워크로드·입력 집합이 양 구성에 적용된다.
- CXL-PNM·PIM-SSD 디바이스가 Enable되어 있다.

### 부하 조건
동일한 추론 요청 집합을 양 구성에서 실행.

### 관련 컴포넌트
- ComputeOffloadExecutor
- RetrievalOffloadExecutor
- ComputeDispatchPlanner
- KVCacheReuseResolver

## 동작

동일 워크로드를 Baseline과 MCR Runtime 구성에서 각각 실행한다. MCR 구성에서는 일부 연산이 CXL-PNM/PIM-SSD로 오프로딩되고 재사용 가능한 KV는 재연산이 생략된다. 양 구성의 GPU 연산량을 측정한다.

## 측정

- 측정 항목: GPU 연산 부하 절감률 (%)
- 측정 공식:

```
절감률 = ([Baseline GPU 연산량] - [MCR GPU 연산량]) / [Baseline GPU 연산량] × 100
(GPU 연산량 = FLOPs 또는 GPU 점유 시간)
```

## 관련 문서

- UC-006 (CXL-PNM 연산 오프로딩)
- UC-007 (PIM-SSD Retrieving 가속 오프로딩)
- UC-002 (Non-contiguous KV 캐시 재사용)
- 컴포넌트: ComputeOffloadExecutor, RetrievalOffloadExecutor
