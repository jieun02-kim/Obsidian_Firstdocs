---
type: literature
source: "Pratik Somaiya, Harit Pandya, Riccardo Polvara, Marc Hanheide, Grzegorz Cielniak. TS-Rep: Self-Supervised Time Series Representation Learning from Robot Sensor Data. 3rd Workshop on Self-Supervised Learning - Theory and Practice (NeurIPS 2022)."
author: "Pratik Somaiya et al. (University of Lincoln, UK; Toshiba Research Europe)"
year: 2022
venue: "NeurIPS 2022 Workshop (Self-Supervised Learning - Theory and Practice)"
impact_factor: "N/A (워크숍 논문)"
tags: [self-supervised, time-series, robot-sensor, representation-learning, triplet-learning, multimodal]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- 실제 로봇에서 수집한 멀티모달·가변 길이(varying-length) 시계열 센서 데이터로부터 표현을 학습하는 자기지도(self-supervised) 방법 **TS-Rep** 제안
- 단순하지만 효과적인 triplet learning 기법 기반: 하나의 시계열을 무작위로 두 구간으로 분할해 anchor/positive를 구성하고, 미니배치 내 다른 시계열에서 무작위 subseries를 뽑아 negative로 사용
- representation space에서의 nearest neighbour를 추가로 활용해 positive의 다양성을 높임
- 이종(heterogeneous) 로보틱스 데이터셋 3종에 대해 clusterability 분석 수행, 학습된 표현을 anomaly detection과 terrain classification에 적용해 검증
- unsupervised 방법 대비 일관되게 우수하며, fully-supervised 방법에 근접하는 성능. baseline 대비 학습 속도도 평균적으로 가장 빠름
- 코드 공개: https://github.com/imprs/TS-Rep

## 메모
- 초록/PDF 1차 정리. "멀티모달 로봇 센서 데이터를 보간·정렬 전처리 없이 표현학습에 바로 활용"하는 접근이라, 본 프로젝트의 비동기 멀티모달 센서 상황과 문제의식이 맞닿아 있음 — [[Learning From Irregularity - Continuous-Time State Space Models for Asynchronous Multimodal UAV Sensor Fusion]]과 비교해 볼 가치 있음 (TS-Rep은 표현학습/이상탐지, 저쪽은 continuous-time SSM 기반 진단이라는 차이)
