---
type: literature
source: "Baodong Wang, Zhen Jia, Yong Tang, Zhenbao Liu. Learning From Irregularity: Continuous-Time State Space Models for Asynchronous Multimodal UAV Sensor Fusion. IEEE Sensors Journal, Vol. 26, No. 12, 15 June 2026, pp. 18863-."
author: "Baodong Wang, Zhen Jia, Yong Tang, Zhenbao Liu (Northwestern Polytechnical University, China)"
year: 2026
venue: "IEEE Sensors Journal"
impact_factor: "4.5, Q1 (2026 JCR 기준)"
tags: [multimodal, sensor-fusion, asynchronous, irregular-sampling, state-space-model, uav, fault-diagnosis]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- 멀티로터 UAV의 로터 고장 진단은 멀티모달 센서 퓨전에 의존하지만, 온보드 항전장비는 버스 중재 지연·이종 샘플링 레이트·전자기 간섭(EMI) 기반 패킷 손실 때문에 근본적으로 비동기적·불규칙 샘플링 데이터를 발생시킴
- 기존 방법들은 강제 보간(interpolation)에 의존하는데, 이 과정에서 초기 로터 손상의 고주파 미세진동 신호가 손상됨을 지적
- **ISFD(Irregularly Sampled Fault Diagnosis)** 패러다임 제안 — 보간 없이 raw하고 불규칙하게 타임스탬프가 찍힌 센서 스트림에서 바로 end-to-end 진단하는 continuous-time state space model 기반 구조
- 아키텍처 구성: (1) time-aware continuous embedding, (2) Ebbinghaus 망각곡선 기반 SSM(state space model) 백본(spectrally bounded projection 포함), (3) 비동기 멀티모달 정렬을 위한 event-driven ODE fusion layer
- 마이크로초 단위 원시 타임스탬프를 보존한 최초의 UAV 고장 데이터셋에서 검증: macro F1-score 89.06%로 최고 보간 기반 baseline 대비 13.74%p 우위. 70% EMI 버스트 패킷 손실 상황에서 baseline들은 10~21%p 성능이 붕괴하는 반면 ISFD는 오히려 +0.68%p 개선 — continuous-time decay matrix의 물리적 정규화 효과를 검증

## 메모
- 초록 기반 1차 정리. "서로 다른 샘플링 레이트/지연을 가진 센서를 보간 없이 직접 융합"하는 접근은, 본 프로젝트가 다루는 비동기 멀티모달 센서 상황(제어 가능 상태 진입을 위한 상태운용 절차)과 문제의식이 가장 근접함 — Ebbinghaus 망각곡선 기반 SSM과 event-driven ODE fusion layer는 구체적 구현 시 우선 검토할 가치가 있음

## 추가 조사 (모달리티 / 소스코드 / 퓨전 기법)

**모달리티**
- 초록에는 IMU·진동계·전류센서 등 구체적인 센서 종류가 명시되어 있지 않음. "온보드 항전장비(avionics)"에서 나오는 이종·비동기 센서 스트림을 대상으로 하며, 자체 구축한 쿼드로터 테스트베드에서 마이크로초 단위 raw 타임스탬프를 보존한 최초의 UAV 고장 데이터셋을 사용했다고만 서술됨
- 정확한 모달리티 목록(센서 종류별 샘플링 레이트 등)은 본문 확인이 필요하나, IEEE Sensors Journal 폐쇄형 접근(closed access) 논문이라 본문은 확인하지 못함 — 향후 원문 입수 시 보강 필요

**소스코드 공개 여부**
- **비공개로 판단됨.** GitHub에서 "Learning From Irregularity" UAV, ISFD(Irregularly Sampled Fault Diagnosis) 등으로 검색했으나 관련 저장소를 찾지 못함
- Semantic Scholar 기준 `openAccessPdf.status: "CLOSED"`, Unpaywall에서도 오픈 액세스 버전 확인 안 됨 → 현재 시점 공개 저장소/프리프린트 없음

**퓨전 기법**
Continuous-time state space model 기반 3단 구조:
1. **Time-aware continuous embedding** — 불규칙 타임스탬프를 보간 없이 그대로 임베딩에 반영
2. **Ebbinghaus 망각곡선 기반 SSM 백본** (spectrally bounded projection 포함) — 시간 경과에 따른 정보 감쇠를 망각곡선 형태의 물리적 감쇠 함수로 모델링해 SSM 상태 전이에 반영
3. **Event-driven ODE fusion layer** — 각 센서 이벤트(비동기 샘플)가 도착하는 시점마다 ODE로 상태를 업데이트하여 멀티모달 정렬·융합을 수행 (고정 타임스텝 grid 불필요)
- 핵심 아이디어: 고정 간격 보간 대신 continuous-time decay matrix로 시간 간격 자체를 정규화 신호로 활용 → 패킷 손실(EMI) 상황에서도 성능이 오히려 개선되는 결과로 이어짐

**서지 확인 정보**
- DOI: [10.1109/JSEN.2026.3691354](https://doi.org/10.1109/JSEN.2026.3691354)
- IEEE Xplore: https://ieeexplore.ieee.org/document/11520605/
