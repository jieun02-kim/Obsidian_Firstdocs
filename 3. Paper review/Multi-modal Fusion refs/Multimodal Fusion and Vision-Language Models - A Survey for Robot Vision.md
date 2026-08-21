---
type: literature
source: "Xiaofeng Han, Shunpeng Chen, Zenghuang Fu, Zhe Feng, Lue Fan, Dong An, Changwei Wang, Li Guo, Weiliang Meng, Xiaopeng Zhang, Rongtao Xu, Shibiao Xu. Multimodal fusion and vision-language models: A survey for robot vision. Information Fusion 126 (2026) 103652."
author: "Xiaofeng Han et al. (Institute of Automation CAS, Beijing University of Posts and Telecommunications, Shandong Computer Science Center)"
year: 2026
venue: "Information Fusion (Elsevier)"
impact_factor: "15.5 (2026 JCR 기준)"
tags: [multimodal, fusion, vision-language-model, survey, robot-vision, slam, manipulation]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- 로봇 비전(robot vision) 태스크를 축으로 한 **task-centric 분석 프레임워크**를 구성해, 멀티모달 퓨전 기법과 Vision-Language Model(VLM)의 적용·발전을 리뷰
- semantic scene understanding 태스크에서 퓨전 방법을 encoder-decoder / attention-based / GNN 세 카테고리로 분류 — [[1. Deep Multimodal Data Fusion|Deep Multimodal Data Fusion]]의 5분류 중 상위 3개와 동일한 축을 로봇 비전 도메인에 특화해 재구성한 형태
- SLAM, 3D 객체 탐지, 내비게이션, 로봇 조작(manipulation) 등 핵심 태스크에서 각 퓨전 전략의 아키텍처 특징과 실제 구현 사례를 분석
- VLM의 발전 경로를 modal alignment 중심의 초기 설계 → 통합적·맥락 인지적(context-aware) 아키텍처로 정리, instruction understanding·로봇 태스크 적응력 향상 추세를 설명
- 널리 쓰이는 데이터셋을 실제 로봇 환경 적용성·한계 관점에서 분석
- cross-modal alignment, 효율적 퓨전, 실시간 배포, domain adaptation을 핵심 과제로 제시하고, self-supervised learning 기반 강건한 표현 학습, 구조화된 공간 메모리, adversarial robustness·human feedback 결합 등을 향후 방향으로 제안

## 메모
- 초록 기반 1차 정리. [[1. Deep Multimodal Data Fusion|Deep Multimodal Data Fusion]]의 일반 taxonomy를 "로봇 비전"이라는 본 프로젝트와 가장 가까운 도메인에 적용한 최신(2026) 서베이 — SLAM/조작(manipulation) 태스크별 퓨전 전략 비교표(원문 참고)가 실제 아키텍처 선택 시 가장 실용적인 참고 자료가 될 것
