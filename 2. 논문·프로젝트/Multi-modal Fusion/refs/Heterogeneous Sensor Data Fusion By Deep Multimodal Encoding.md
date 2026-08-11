---
type: literature
source: "Zuozhu Liu, Wenyu Zhang, Shaowei Lin, Tony Q.S. Quek. Heterogeneous Sensor Data Fusion By Deep Multimodal Encoding. IEEE Journal of Selected Topics in Signal Processing, Vol. 11, No. 3, April 2017, pp. 479-."
author: "Zuozhu Liu, Wenyu Zhang, Shaowei Lin, Tony Q.S. Quek (Singapore University of Technology and Design, Cornell University)"
year: 2017
venue: "IEEE Journal of Selected Topics in Signal Processing (JSTSP)"
impact_factor: "15.70 (2024 JCR, 최신 공표값 / 게재 당시 값 아님)"
tags: [multimodal, sensor-fusion, missing-data-imputation, shared-representation, wireless-sensor-network]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- 이종 센서 데이터 퓨전의 두 난제: (1) 결측값이 있는 데이터로부터 학습, (2) 멀티모달 데이터의 shared representation 학습을 통한 추론/예측 성능 향상
- **Deep Multimodal Encoder(DME)** 제안 — 센서 데이터 압축, 결측 데이터 대치(imputation), 새로운 모달리티 예측을 하나의 프레임워크로 처리
- 기존 방법이 modality 내부(intra-modal) 상관관계만 포착하는 것과 달리, DME는 얕은 층에서 intra-modal, 깊은 층에서 modality 간(inter-modal) 상관관계까지 함께 포착 → 센서 데이터의 통계적 구조를 더 잘 활용해 압축
- 새로운 목적함수를 도입해 결측 데이터 대치(imputation)에서 강점을 보임
- 학습된 shared multimodal representation을 다른 모달리티 예측에 직접 활용 가능
- 40개 노드 농업 센서 네트워크(3개 모달리티) 실증 실험: 결측 데이터 대치 RMSE가 KNN·sparse PCA 등 전통 기법 대비 20% 수준, 결측률이 달라져도 강건. 80% 결측 데이터로 학습한 2.1% 압축 표현만으로 습도·조도에서 온도 모달리티를 RMSE 7℃로 복원

## 메모
- 초록 기반 1차 정리. "결측된 모달리티를 다른 모달리티로부터 복원"하는 아이디어는 본 프로젝트의 metadata 구조([MetaData - Topology/Module/State Info]) 설계 시, 센서 일부가 비활성/고장 상태일 때 나머지 모달리티로 상태를 추정하는 방식의 근거로 참고 가능
