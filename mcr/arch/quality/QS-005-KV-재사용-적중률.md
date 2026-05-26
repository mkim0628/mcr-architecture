# QS-005-KV-재사용-적중률

## 개요

### Quality Scenario ID
QS-005

### 제목
KV 재사용 적중률

### 설명
Non-contiguous KV 캐시 재사용(UC-002)으로 재연산 없이 재사용된 KV의 비율.

### 품질 속성
성능 (자원 효율)

## 환경

### 시스템 상태
MCR Runtime이 가동 중이며, KVCacheRegistry에 기존 KV 캐시 블록의 메타데이터·인덱스가 유지되고 있다.

### 초기 조건
- 재사용 후보가 되는 기존 KV 캐시가 메모리 계층에 존재한다.
- 토큰 위치가 부분적으로 겹치거나 불일치하는 요청들이 유입된다.

### 부하 조건
반복·중첩 컨텍스트를 포함하는 워크로드.

### 관련 컴포넌트
- KVCacheReuseResolver
- KVCacheRegistry

## 동작

서빙 프레임워크가 토큰 시퀀스와 KV 캐시 핸들을 전달하면, 시스템은 KVCacheRegistry를 조회하여 위치 불일치를 허용한 재사용 가능 영역을 식별한다. 재사용으로 충족된 KV와 재연산이 필요한 KV를 구분하여 집계한다.

## 측정

- 측정 항목: KV 재사용 적중률 (%)
- 측정 공식:

```
재사용 적중률 = [재사용으로 충족된 KV 토큰 수] / [전체 요구 KV 토큰 수] × 100
```

## 관련 문서

- UC-002 (Non-contiguous KV 캐시 재사용)
- 컴포넌트: KVCacheReuseResolver, KVCacheRegistry
