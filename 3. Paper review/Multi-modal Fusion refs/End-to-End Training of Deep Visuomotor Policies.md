---
type: literature
source: "Sergey Levine, Chelsea Finn, Trevor Darrell, Pieter Abbeel. End-to-End Training of Deep Visuomotor Policies. Journal of Machine Learning Research 17 (2016) 1-40."
author: "Sergey Levine, Chelsea Finn, Trevor Darrell, Pieter Abbeel (UC Berkeley)"
year: 2016
venue: "Journal of Machine Learning Research (JMLR)"
impact_factor: "6.8 (2026 JCR 기준, 게재 당시 값 아님)"
tags: [multimodal, visuomotor-policy, reinforcement-learning, robot-manipulation, end-to-end]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- 핵심 질문: "지각(perception)과 제어(control)를 분리 학습하는 것보다 end-to-end로 함께 학습하면 성능이 더 좋은가?"
- raw 이미지 관측값을 로봇 모터 토크로 직접 매핑하는 정책을 학습하는 방법을 제안 — 92,000개 파라미터를 가진 CNN으로 정책을 표현
- **guided policy search**를 사용: policy search 문제를 지도학습(supervised learning) 문제로 변환하고, trajectory-centric 강화학습 기법으로 지도 신호(supervision)를 생성
- 병뚜껑 돌려 닫기 등 시각-제어 간 정교한 협응이 필요한 실제 조작(manipulation) 태스크에서 검증, 기존 policy search 기법들과 시뮬레이션 비교 결과도 제시

## 메모
- 초록 기반 1차 정리. 이미지(모달리티)를 별도 지각 파이프라인으로 분리하지 않고 제어 신호까지 end-to-end로 엮는 구조는, 본 프로젝트에서 "모달리티별 인코딩 → 상태 판단 → 제어" 파이프라인을 얼마나 분리/통합할지 설계할 때 참고할 만한 대비 사례
