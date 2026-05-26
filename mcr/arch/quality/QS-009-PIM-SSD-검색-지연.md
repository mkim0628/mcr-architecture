# QS-009-PIM-SSD-검색-지연

## 개요

### Quality Scenario ID
QS-009

### 제목
PIM-SSD 검색 지연

### 설명
대용량 데이터 검색을 PIM-SSD로 In-Storage 오프로딩(UC-007)했을 때의 검색 지연.

### 품질 속성
성능 (지연)

## 환경

### 시스템 상태
PIM-SSD 디바이스가 Enable되어 있고, 검색 대상 데이터셋이 PIM-SSD에 적재되어 있다.

### 초기 조건
- 검색 질의와 대상 데이터셋 참조가 주어진다.
- 검색 연산이 PIM-SSD에서 지원되는 형태이다.

### 부하 조건
대용량 데이터셋에 대한 검색 질의가 유입되는 워크로드.

### 관련 컴포넌트
- RetrievalOffloadExecutor
- PIMSSDInterface

## 동작

서빙 프레임워크가 검색 가속을 요청하면, 시스템은 PIM-SSD에 In-Storage 검색 실행을 요청하고 결과를 수신하여 반환한다. 검색 질의 전달부터 결과 반환까지의 시간을 측정한다.

## 측정

- 측정 항목: PIM-SSD 검색 지연 (ms)
- 측정 공식:

```
검색 지연 = [검색 결과 반환 시각] - [검색 질의 전달 시각]
```

## 관련 문서

- UC-007 (PIM-SSD Retrieving 가속 오프로딩)
- 컴포넌트: RetrievalOffloadExecutor, PIMSSDInterface
