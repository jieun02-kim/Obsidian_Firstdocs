---
type: literature
source: "Zihao Li, Xiao Lin, Zhining Liu, Jiaru Zou, Ziwei Wu, Lecheng Zheng, Dongqi Fu, Yada Zhu, Hendrik Hamann, Hanghang Tong, Jingrui He. Language in the Flow of Time: Time-Series-Paired Texts Weaved into a Unified Temporal Narrative. ICLR 2026 (arXiv:2502.08942v3)."
author: "Zihao Li et al. (University of Illinois Urbana-Champaign, Meta, IBM Research)"
year: 2026
venue: "ICLR 2026"
impact_factor: "N/A (학회논문)"
tags: [multimodal, time-series, text, llm, forecasting, imputation]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- Platonic Representation Hypothesis(서로 다른 모달리티의 표현이 공유된 공간으로 수렴한다는 가설)에 기반해, 시계열과 짝지어진(paired) 텍스트의 통합을 재조명
- 시계열-페어드 텍스트가 원본 시계열과 유사한 주기적(periodic) 속성을 자연스럽게 갖는다는 점을 발견
- 이 통찰을 바탕으로 **TaTS(Texts as Time Series)** 제안 — 텍스트를 시계열의 또 다른 수치 변수(보조 변수)로 취급
- 기존 수치 전용(numerical-only) 시계열 모델에 아키텍처 변경 없이 그대로 plug-in 가능
- 멀티모달 시계열 예측(forecasting) + 결측치 보완(imputation) 양쪽 벤치마크에서 검증, 모델 구조 수정 없이 예측 성능 향상
- 코드 공개: https://github.com/iDEA-iSAIL-Lab-UIUC/TaTS

## 메모
- 초록 기반 1차 정리. [[Multi-modal Time Series Analysis A Tutorial and Survey]]에서 input-stage fusion 사례(TaTS)로 인용된 논문 — 텍스트를 별도 인코더/크로스어텐션 없이 "추가 채널"로 다루는 가장 단순한 형태의 input-level fusion이라 baseline/비교군으로 검토할 가치 있음
