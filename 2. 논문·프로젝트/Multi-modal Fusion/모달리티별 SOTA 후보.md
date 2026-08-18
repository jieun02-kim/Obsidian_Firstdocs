프로젝트: [[Multi-modal Fusion]]

### 시계열(센서 데이터)

이상탐지·상태 변화 감지가 목표에 포함된다면, 시간축 상관관계뿐 아니라 센서 간 공간적 상관관계도 함께 고려하는 spatial-temporal Transformer 구조

최근 patch 기반 Transformer 인코더가 LSTM/TCN 대비 대부분의 벤치마크에서 우위PatchTST는 패치 토큰과 채널 독립 인코딩을 활용해 시계열 예측, 분류, 표현학습에서 최신 성능을 보이며, 단일 Transformer 인코더가 모든 채널에 걸쳐 파라미터를 공유하면서 각 단변량 패치 시퀀스를 독립적으로 처리

결측/불규칙 샘플링이 있다면 규칙적 샘플링에는 절대적 위치 인코딩을, 불규칙 샘플링에는 타임스탬프 임베딩이나 상대적 시간 인코딩을 사용하는 걸 권장

### 이미지

사전학습된 ViT를 인코더로 쓰는 게 사실상 표준

MAE (Masked Autoencoder): 기계 부품 손상, 외형 마모 등 세부적인 시각적 미세 구조(Fine-grained visual feature)를 파악할 때 사용.

CLIP-ViT: 작업 환경의 공간적 맥락, 로봇의 배치 및 객체 식별과 같은 고차원 의미적 맥락(Semantic feature) 추출.

### 메타데이터(설정파일)

로봇 HW 스펙, 펌웨어 버전, 네트워크 설정, 캘리브레이션 매개변수 등 이종(Heterogeneous) 정보 인코딩

시퀀스 인코더보다 구조화 데이터 임베딩 접근

필드별(디바이스 타입, 펌웨어 버전, 파라미터 값 등) 임베딩 후 concat하거나, 작은 MLP/tabular transformer로 하나의 벡터로 압축하는 방식이 일반적

메타데이터는 시계열·이미지보다 정보 밀도가 낮고 변화가 드물기 때문에, 융합 단계에서 "보조 정보"로 취급해 다른 두 모달리티의 attention query를 보정하는 conditioning 역할로 쓰는 설계가 많이 채택



SOTA

iTransformer (ICLR 2024/2025 SOTA) : 기존 PatchTST처럼 시간 축만 잘라내던 방식과 달리, 센서 변수(채널) 차원을 토큰화(Inverted Transformer)함.

Timer / UniTS (2025 Foundation Models for Time Series) : 다양한 산업용 센서 패턴을 사전학습(Pre-train)한 대형 시계열 기반 모델로, 로봇 플릿 환경에 Zero-Shot / Few-Shot으로 적응.