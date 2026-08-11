---
type: literature
source: "Anthony Bisulco, Jeremy Wang, Kostas Daniilidis, Randall Balestriero, Pratik Chaudhari. OctoSense: Self-Supervised Learning for Multimodal Robot Perception. arXiv:2606.27317v1 [cs.CV], 2026."
author: "Anthony Bisulco et al. (University of Pennsylvania GRASP Lab, Brown University)"
year: 2026
venue: "arXiv preprint (cs.CV)"
impact_factor: "N/A (arXiv preprint, 미게재)"
tags: [multimodal, sensor-fusion, self-supervised-learning, robot-perception, masked-autoencoder]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- Stereo RGB·이벤트 카메라·LiDAR·열화상 카메라·IMU·RTK-GPS·proprioception(차량 CAN bus, 사족보행 로봇 관절각)까지 포함한 오픈소스 멀티센서 플랫폼 **OctoSense**와, 다양한 시간대·환경(센서 열화 상황 포함)에서 수집한 59시간 분량의 시간 동기화 주행 데이터셋을 공개
- 센서마다 표현 방식·주파수·지연시간·노이즈 특성이 다른 실세계 로보틱스 데이터에 대해 **멀티모달 자기지도학습(self-supervised learning)**을 적용
- 핵심 구조는 "late-fusion" masked autoencoder — (1) 센서별 시공간 특성을 반영한 modality-specific tokenizer 사용, (2) 추론 시 modality별 토큰을 캐싱해 새 측정값이 들어올 때마다 증분 처리 가능
- 속도가 빠름(NVIDIA 5090에서 6.68ms, Orin NX에서 112ms), optical flow·depth·semantic segmentation·ego-motion(이동/회전/조향각) 추정에서 기존 이미지 전용 foundation model보다 우수한 성능
- 야간이나 센서 열화 상황에서도 강건한 예측 성능을 보임

## 메모
- 초록 기반 1차 정리. "다양한 주파수·지연·노이즈를 가진 이종 센서를 어떻게 하나의 학습 파이프라인에 태울 것인가"라는 문제의식이 본 프로젝트의 Topology/Module/State Info 축 설계와 직접 맞닿아 있음 — modality-specific tokenizer + 캐싱 방식은 실시간 상태운용 절차 구현 시 참고할 만함
