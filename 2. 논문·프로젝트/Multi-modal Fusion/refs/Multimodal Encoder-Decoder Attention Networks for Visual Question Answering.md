---
type: literature
source: "Chongqing Chen, Dezhi Han, Jun Wang. Multimodal Encoder-Decoder Attention Networks for Visual Question Answering. IEEE Access, DOI: 10.1109/ACCESS.2020.2975093, 2020."
author: "Chongqing Chen, Dezhi Han (Shanghai Maritime University), Jun Wang (University of Central Florida)"
year: 2020
venue: "IEEE Access"
impact_factor: "4.2, Q2 (2026 JCR 기준)"
tags: [multimodal, encoder-decoder, attention, visual-question-answering]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- VQA(Visual Question Answering)는 컴퓨터 비전과 자연어처리가 결합된 멀티모달 태스크 — 이미지의 시각 정보와 질문의 텍스트 정보를 세밀하고 동시적으로 이해하는 것이 핵심
- **Multimodal Encoder-Decoder Attention Networks(MEDAN)** 제안 — MEDA(Multimodal Encoder-Decoder Attention) 레이어를 깊이 방향으로 쌓은 구조
- 각 MEDA 레이어는 (1) 질문의 self-attention을 모델링하는 Encoder 모듈, (2) 질문에 의해 유도되는(question-guided) attention과 이미지의 self-attention을 모델링하는 Decoder 모듈로 구성 — 질문 속 키워드와 이미지 내 중요 객체 영역을 연결
- VQA-v2 벤치마크에서 SOTA 성능 달성 (Adam: test-std 71.01%, AdamW: test-dev 70.76%)
- 다양한 ablation study로 MEDAN의 효과 원인을 분석

## 메모
- 초록 기반 1차 정리. [[Deep Multimodal Data Fusion]] 분류 기준으로는 "Attention 기반"의 대표적 encoder-decoder 결합 구조 — 질문(텍스트)이 이미지에 대해 cross-attention으로 질의하는 패턴은, 본 프로젝트에서 한 모달리티를 쿼리로 삼아 다른 모달리티를 참조하는 구조를 설계할 때 참고할 만한 사례
