---
type: literature
source: "Yao-Hung Hubert Tsai, Shaojie Bai, Paul Pu Liang, J. Zico Kolter, Louis-Philippe Morency, Ruslan Salakhutdinov. Multimodal Transformer for Unaligned Multimodal Language Sequences. ACL 2019."
author: "Yao-Hung Hubert Tsai et al. (Carnegie Mellon University, Bosch Center for AI)"
year: 2019
venue: "ACL 2019 (학회논문)"
impact_factor: "N/A (학회논문, IF 대상 아님)"
tags: [multimodal, transformer, cross-modal-attention, alignment, time-series]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- 인간 언어는 자연어·표정·음성 등 여러 모달리티가 섞인 형태 — 이를 모델링할 때 두 가지 난제: (1) 모달리티별 샘플링 레이트가 달라 발생하는 데이터 비정렬(non-alignment), (2) 모달리티 간 장거리 의존성(long-range dependency)
- **Multimodal Transformer(MulT)** 제안 — 데이터를 명시적으로 정렬하지 않고 end-to-end로 위 문제들을 해결
- 핵심은 **directional pairwise crossmodal attention**: 서로 다른 타임스텝에 걸친 멀티모달 시퀀스 간 상호작용에 주목하며, 한 모달리티의 스트림을 다른 모달리티로 잠재적으로(latently) 적응시킴
- 정렬된(aligned) 데이터와 비정렬(non-aligned) 데이터 모두에서 기존 SOTA 대비 큰 폭으로 성능 향상
- 실험적으로 crossmodal attention 메커니즘이 모달리티 간 상관된 신호를 실제로 포착함을 확인

## 메모
- 초록 기반 1차 정리. [[Multi-modal Time Series Analysis A Tutorial and Survey]]가 정리한 "Intermediate-level Alignment"의 cross-attention 항목과 직접 대응하는 원 논문 — 시계열/센서처럼 샘플링 레이트가 다른 모달리티를 명시적 정렬(interpolation) 없이 융합하는 대표 구현체로, 본 프로젝트의 비동기 센서 퓨전 설계 시 참고할 만함
