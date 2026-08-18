---
type: literature
source: "Songtao Li, Hao Tang. Multimodal Alignment and Fusion: A Survey. arXiv:2411.17040v2 [cs.CV], 2025."
author: "Songtao Li (Northeastern University, work done at Peking University), Hao Tang (Peking University)"
year: 2025
venue: "arXiv preprint (cs.CV)"
impact_factor: "N/A (arXiv preprint, 미게재)"
tags: [multimodal, alignment, fusion, survey, contrastive-learning, attention, llm]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- 텍스트·이미지·오디오·비디오 등 모달리티 데이터가 폭발적으로 늘어나는 상황에서, 최근 멀티모달 정렬(alignment)·퓨전(fusion) 연구를 종합적으로 리뷰한 서베이
- 특정 모달리티나 제한된 퓨전 전략에 집중했던 기존 서베이와 달리, **구조 중심(structure-centric) + 방법론 중심(method-driven)의 일반화 가능한 프레임워크**를 제시
- 구조적 관점: data-level / feature-level / output-level fusion으로 분류
- 방법론적 관점: statistical, kernel-based, graphical, generative, contrastive, attention-based, LLM-based 방법으로 분류 — 260편 이상의 관련 연구를 검토해 정리
- cross-modal misalignment, 연산 병목, 데이터 품질 문제, modality gap 등 핵심 난제와 최근 대응 연구도 함께 다룸
- 소셜미디어 분석, 의료 영상, 감정 인식, embodied AI 등 실제 응용 사례로 멀티모달 시스템의 실효성을 보임
- 확장성·강건성·범용성 향상을 위한 향후 연구 방향 제시

## 메모
- 초록 기반 1차 정리. [[Deep Multimodal Data Fusion]]의 "메인 메커니즘(딥러닝 기법) 기준 5분류"와 비교하면, 이 논문은 구조(data/feature/output-level) × 방법론(statistical~LLM-based) 두 축으로 훨씬 세분화된 taxonomy를 제공 — 최신(2025) 서베이인 만큼 LLM-based fusion 등 최신 트렌드를 확인할 때 우선 참고할 만함
