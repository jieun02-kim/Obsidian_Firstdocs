---
type: literature
source: "Julian Nubert, Turcan Tuna, Jonas Frey, Cesar Cadena, Katherine J. Kuchenbecker, Shehryar Khattak, Marco Hutter. Holistic Fusion: Task- and Setup-Agnostic Robot Localization and State Estimation with Factor Graphs. arXiv:2504.06479v2 [cs.RO], 2026."
author: "Julian Nubert et al. (ETH Zurich)"
year: 2026
venue: "arXiv preprint (cs.RO)"
impact_factor: "N/A (arXiv preprint, 미게재)"
tags: [multimodal, sensor-fusion, robot-localization, factor-graph, state-estimation]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- 특정 태스크·센서 조합에 맞춰 하드코딩되는 기존 센서 퓨전 방식과 달리, **어떤 태스크/로봇 셋업에도 재사용 가능한 범용 센서 퓨전 프레임워크**(오픈소스)를 제안
- 센서 퓨전을 (1) 로봇의 local/global state 추정과 (2) 이론상 무제한 개수의 동적 변수(레퍼런스 프레임 자동 정렬 포함) 추정을 결합한 하나의 factor-graph 최적화 문제로 정식화
- 서로 다른 좌표계(frame)를 기준으로 표현된 임의 개수의 절대(absolute)/로컬(local)/랜드마크(landmark) 측정값을 직접 상태 변수로 포함시켜 융합 — 각 변수의 시간적 변화를 random walk로 모델링
- local smoothness/consistency를 별도로 신경 써서 상태 추정값이 튀는(estimation jump) 문제를 방지
- 일반 로봇 하드웨어에서 저지연·부드러운 온라인 상태 추정과, IMU 측정 주기 수준의 저드리프트 global localization을 동시에 제공
- 서로 다른 태스크 요구사항을 가진 3종의 로봇 플랫폼, 5가지 실세계 시나리오에서 효과 검증

## 메모
- 초록 기반 1차 정리. Multi-modal Fusion 프로젝트의 "센서 퓨전 아키텍처" 설계 시, **모달리티/태스크에 종속되지 않는 범용 프레임워크**를 어떻게 구성하는지 참고할 사례로 적합 — 특히 factor-graph 기반 상태 변수 정의 방식은 metadata → 상태운용 절차 설계에 참고 가치 있음
