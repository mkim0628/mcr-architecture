# 과제 정의서: AI Runtime Framework for Memory-Centric System
## 1. 과제 개요
과제명: AI Runtime Framework for Memory-Centric System
과제 목표: 메모리 중심 시스템에서 AI Agent의 기억 성능 향상을 위한 동적 스케줄링 최적화 알고리즘 연구
연구 배경:
* PIM/PNM 디바이스, 시스템 메모리(DRAM), CXL 인터페이스 확장 메모리, SSD가 혼재된 이기종 환경 대응 필요
* 워크로드 특성에 따른 효율적 자원 할당 및 데이터 이동/연산 비용 최소화 런타임 메커니즘 개발
* 자사 제품의 기술적 가치와 경쟁력 제고를 위한 기반 기술 확보

## 2. 주요 연구 활동 (Activity)
### 2.1 Inference Orchestration
[연구 내용]
워크로드 특성(요청 패턴, 토큰 길이, 반복성)과 시스템 상태(메모리 계층, 용량, 비용)를 인지하는 Cost-aware Memory-centric Inference Scheduling 연구. GPU 연산을 최소화하고 KV 캐시의 배치, 재사용, 압축을 동적으로 최적화하여 End-to-End 추론 처리량 및 시스템 효율 극대화.

[Initiative]
Cost-aware Memory-centric Inference Scheduling: 성능 Cost 모델 기반의 메모리 및 Load 배치 Policy 스케줄링
KV 캐시 재사용 고도화: Non-contiguous KV 캐시 재사용 알고리즘 (토큰 위치가 일치하지 않아도 재사용 가능)
KV 캐시 압축 적용

### 2.2 Computable-Memory 최적화
[연구 내용]
CXL-PNM 활용 LLM 가속 연구

[Initiative]
1. System Modeling 기반 가속 전략 연구
  * Baseline(GPU 중심) 시스템 모델 및 성능 분석
  * Future 시스템(CPU w/ DRAM, CXL switch w/ CXL-PNM) 모델 및 가속 분석
  * LLM Serving Framework 실측 성능 반영을 통한 분석 고도화
  * 가속 알고리즘 도출 (Pipelining, Tiling, Data Placement 등)
2. 실제 시스템 기반 성능 최적화 연구
* Scale-down 성능 평가 시스템 구축 (MCR TestBed, Latest LLM Serving F/W)
* CXL-PNM 장치 Enable 및 Attention 연산 Offloading
* 가속 알고리즘 도출 및 검증
3. Emulation 기반 가속 전략 연구
* QEMU 활용 Future CXL Switch w/ CXL-PNM 에뮬레이션 환경 확보
* Future 가속 시스템 성능 평가 환경 구성
* 가속 알고리즘 도출 및 검증

### 2.3 Tiered-Memory 최적화
[연구 내용]
Tiered Memory 내 KV Cache의 최적 Data Placement를 통한 TTFT(Time To First Token) 최적화 알고리즘 연구

[Initiative]
* KV Cache Classification/Migration 알고리즘: 데이터 성격에 따른 분류 및 이동 최적화
* KV Cache Classification 정책 결정 알고리즘