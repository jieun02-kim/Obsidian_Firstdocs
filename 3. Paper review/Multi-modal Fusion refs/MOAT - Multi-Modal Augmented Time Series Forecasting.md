---
type: literature
source: "Geon Lee, Wenchao Yu, Wei Cheng, Haifeng Chen. MoAT: Multi-Modal Augmented Time Series Forecasting. OpenReview (ICLR 2024 submission)."
author: "Geon Lee, Wenchao Yu, Wei Cheng, Haifeng Chen (NEC Laboratories America 등으로 추정)"
year: 2024
venue: "OpenReview preprint (ICLR 2024 제출작, double-blind review)"
impact_factor: "N/A (preprint)"
tags: [multimodal, time-series, forecasting, data-augmentation, trend-seasonal-decomposition]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- 시계열 예측에서 학습 샘플 부족(data scarcity) 문제를, 시계열과 함께 존재하는 다른 모달리티 정보를 활용해 완화하고자 함
- **MoAT** 제안 — feature-wise augmentation과 sample-wise augmentation을 전략적으로 결합해 멀티모달 표현 학습을 강화
- 모든 모달리티에 걸쳐 공통으로 trend-seasonal decomposition을 적용한 뒤 최종 예측을 위해 정보를 융합(output-level fusion에 가까움)
- COVID-19 확진자 수 예측처럼 데이터가 부족한 시나리오에서 SOTA 대비 MSE를 6.5%~71.7% 감소시켜 효과성·강건성을 입증
- 코드/데이터셋: anonymous.4open.science/r/MoAT-201E (익명 리뷰용 링크로 게재됨, 현재 시점 유효성 미확인)

## 메모
- 초록/PDF 1차 정리. PDF 자체는 "Under review as a conference paper at ICLR 2024"로 표기된 익명(double-blind) 버전이며, 저자 정보는 이후 공개된 OpenReview 페이지(https://openreview.net/forum?id=uRXxnoqDHH) 기준으로 보강함
- [[Multi-modal Time Series Analysis A Tutorial and Survey]]에서 output-stage fusion의 대표 사례로 인용됨 — 1단계(모달리티별 decomposition+예측) → 2단계(MLP 기반 오프라인 종합)의 2단계 구조가 특징
- 2단계(MLP 기반 오프라인 종합)에서 서로 다른 구성 요소들을 동적으로 융합하고, 상대적 기여도에 기반해 최종 예측을 산출
