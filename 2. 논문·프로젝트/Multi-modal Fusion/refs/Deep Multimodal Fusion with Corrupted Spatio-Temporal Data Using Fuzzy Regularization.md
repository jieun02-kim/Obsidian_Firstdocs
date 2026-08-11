---
type: literature
source: "Diyar Altinses, Andreas Schwung. Deep multimodal fusion with corrupted spatio-temporal data using fuzzy regularization. IECON 2023 - 49th Annual Conference of the IEEE Industrial Electronics Society, DOI: 10.1109/IECON51785.2023.10312522."
author: "Diyar Altinses, Andreas Schwung (South Westphalia University of Applied Sciences)"
year: 2023
venue: "IECON 2023 (IEEE 학회논문)"
impact_factor: "N/A (학회논문, IF 대상 아님)"
tags: [multimodal, sensor-fusion, fuzzy-regularization, robustness, industrial, corrupted-data]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- "모달리티는 많을수록 좋다"는 통념과 달리, 손상된(corrupted) 센서 신호를 보정하는 연구는 부족하다는 문제의식에서 출발
- 센서 오작동, 부정확성, 제한된 공간 커버리지, 불확실성 등 **상대적인 센서 약점을 보완**하도록 설계된 새로운 정규화(regularization) 기법을 제안
- 이미지·시계열 모달리티에 특화된 augmentation 전략을 사용해, 데이터가 적은 산업 고장(failure) 케이스를 보강 — 희소 사례가 모델 예측에 부정적 영향을 주는 것을 방지
- 핵심 기법은 **fuzzy regularizer**: 신호 품질에 따라 activation의 강도를 조절 → 여러 모달리티에서 발생하는 교란(disturbance)을 activation 패턴으로 식별 가능
- 시뮬레이션된 Universal Robots UR5 데이터셋 실험에서 모델의 안정성·정확도·불확실성/고장 상황에 대한 일반화 성능 향상을 확인, 구조 복잡도를 늘리지 않고도 성능 개선 가능함을 보임

## 메모
- 초록 기반 1차 정리. 실제 로봇 환경에서 센서 고장/노이즈가 항상 발생할 수 있다는 전제하에, **신호 품질 기반으로 modality별 가중치를 동적으로 조절**하는 아이디어는 본 프로젝트의 상태운용 절차(제어 가능 상태 진입) 설계와 밀접 — "Deep Multimodal Data Fusion" 서베이가 짚은 Future Direction(Missing/Noisy modality 대응)의 구체적 구현 사례로 볼 수 있음
