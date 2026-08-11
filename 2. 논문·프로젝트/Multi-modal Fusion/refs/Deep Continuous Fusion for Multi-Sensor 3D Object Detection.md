---
type: literature
source: "Ming Liang, Bin Yang, Shenlong Wang, Raquel Urtasun. Deep Continuous Fusion for Multi-Sensor 3D Object Detection. ECCV 2018."
author: "Ming Liang et al. (Uber Advanced Technologies Group, University of Toronto)"
year: 2018
venue: "ECCV 2018 (학회논문)"
impact_factor: "N/A (학회논문, IF 대상 아님)"
tags: [multimodal, sensor-fusion, 3d-object-detection, autonomous-driving, continuous-convolution]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-11
---

## 핵심 요약
- LiDAR와 카메라를 함께 활용해 정확한 3D 위치 추정을 수행하는 end-to-end 학습형 3D 객체 탐지기 제안
- 핵심은 **continuous convolution 기반 continuous fusion layer** — 서로 다른 해상도의 이미지 feature map과 LiDAR feature map을 융합
  - discrete-state 이미지 특징과 continuous geometric 정보(3D 좌표)를 동시에 인코딩해, 해상도가 다른 두 modality 간 정보 손실 없이 결합
- 기존 방식들은 카메라로 후보 영역(proposal)을 만들고 LiDAR로 최종 위치를 확정하는 cascading 구조라 2D 탐지 성능에 병목이 걸리는 반면, 본 논문은 두 센서 입력에 대한 joint reasoning을 가능하게 함
- KITTI 및 대규모 3D 객체 탐지 벤치마크에서 기존 SOTA 대비 유의미한 성능 향상 확인

## 메모
- 초록 기반 1차 정리. 해상도가 다른 이종 센서(카메라 dense vs LiDAR sparse) 데이터를 feature-level에서 정렬 없이 융합하는 continuous convolution 아이디어는, 본 프로젝트에서 시간/공간 해상도가 다른 모달리티를 다룰 때 intermediate fusion 전략 후보로 참고할 만함
