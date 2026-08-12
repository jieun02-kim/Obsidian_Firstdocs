---
type: literature
source: "Jiahao Wang, Mingyue Cheng, Qingyang Mao, Yitong Zhou, Daoyu Wang, Qi Liu, Feiyang Xu. TableTime: Reformulating Time Series Classification as Training-Free Table Understanding with Large Language Models. In Proceedings of the 34th ACM International Conference on Information and Knowledge Management (CIKM '25), 2025. https://doi.org/10.1145/3746252.3761056"
author: "Jiahao Wang et al. (University of Science and Technology of China; iFLYTEK)"
year: 2025
venue: "CIKM 2025 (ACM), 2025.11.10-14, Seoul"
impact_factor: "N/A (학회논문)"
tags: [llm, time-series, classification, table-understanding, training-free, multimodal]
project: "[[Multi-modal Fusion]]"
created: 2026-08-11
updated: 2026-08-12
---

# TableTime: Reformulating Time Series Classification as Training-Free Table Understanding with Large Language Models

- **교신저자**: Mingyue Cheng
- **코드**: [https://github.com/realwangjiahao/TableTime](https://github.com/realwangjiahao/TableTime)

---

## Abstract

### 연구 배경

LLM을 MTSC(다변량 시계열 분류, Multivariate Time Series Classification)에 적용하는 접근이 확산됨. 기존 방법 대다수는 수치형 시계열을 LLM의 잠재 공간(latent space)에 인코딩하여 LLM의 의미 공간(semantic space)과 정렬시키는 방식 채택.

#### 기존 방법의 3가지 한계

1. 시간적 정보(temporal) 및 채널별 정보(channel-specific) 반영 어려움 — 둘 다 다변량 시계열의 핵심 구성 요소
2. 학습된 표현 공간을 LLM 의미 공간과 정렬시키는 것 자체가 큰 난제
3. 태스크별 재학습(task-specific retraining) 요구 → LLM의 일반화 능력에도 불구하고 training-free 추론 불가능

### 제안 방법: TableTime

MTSC를 **테이블 이해(table understanding) 태스크**로 재정의하는 프레임워크.

#### 핵심 전략 3가지

1. **표 형식 통일**: 시계열을 tabular 형태로 표현 → model-centric에서 data-centric 접근으로 전환
2. **텍스트 인코딩**: 시계열을 텍스트 포맷으로 표현 → LLM 의미 공간과의 원활한 정렬 도모
3. **지식-태스크 이중 구동 추론 프레임워크**: 문맥 정보(contextual information) + 전문가 수준 추론 가이드(expert-level reasoning guidance) 통합 → LLM 추론 능력 강화 및 training-free 분류 가능케 함

### 실험 검증

UEA 아카이브 기반 공개 벤치마크 10개 데이터셋에서 광범위한 실험 수행. TableTime이 MTSC의 새로운 패러다임이 될 잠재력을 입증함.


## Intro

### 배경

다변량 시계열(multivariate time series)은 여러 속성에 걸쳐 시간에 따라 관측되는 이벤트 시퀀스로, 의료(ECG 등), 산업, 인간 행동 인식 등 다양한 도메인에서 등장. 이 중 MTSC(다변량 시계열 분류)는 학계·산업계 모두에서 주목받는 핵심 문제.

### 기존 MTSC 접근법의 흐름

1. **전통적 방법**: DTW(Dynamic Time Warping) + K-NN — 길이가 다른 시계열 정렬에는 효과적이나 숨겨진 특징 포착에 취약
2. **머신러닝 방법**: SVM, Random Forest — 수작업 특징(handcrafted feature)에 의존, 정상성(stationarity)을 가정해 동적이고 다양한 데이터에 취약
3. **딥러닝 방법**: CNN 기반, Transformer 기반 — 특징 공학 필요성은 줄였지만 대량의 라벨 데이터에 의존

### LLM 기반 접근의 등장과 한계

LLM은 복잡한 시퀀스에 대한 패턴 인식·추론 능력을 보여 시계열 분석에도 적용되기 시작. 크게 두 갈래로 구분:
- **Prompt 기반**: PromptCast 등 — task를 문장-투-문장(sentence-to-sentence) 형식으로 구성해 LLM에 직접 적용
- **Retraining 기반**: LLM 파라미터 일부/전체를 특정 태스크에 맞게 수정

#### LLM 기반 방법의 4가지 병목

1. 수치형 시계열과 LLM의 텍스트 의미 공간(semantic space) 간 불일치
2. 시간적 동역학(temporal dynamics) 및 채널별 특징(channel-specific feature) 포착 어려움
3. 대규모 파인튜닝에 따른 높은 계산 비용
4. LLM의 추론 능력을 충분히 끌어내지 못함

### 효과적인 LLM 기반 MTSC 방법의 요건 (저자 제시)

1. 수치형 시계열을 LLM의 텍스트 의미 공간과 정렬
2. 시간적 일관성(temporal consistency)과 채널 간 특징(inter-channel feature)을 함께 추출
3. 사전학습된 world knowledge를 활용한 training-free 분류
4. 논리적 관계·데이터 내 의존성을 다루는 강한 추론 능력

### 제안: TableTime

Table understanding 기반 training-free 분류 프레임워크.
- 수치형 시계열 → **tabular 형식으로 변환** (시간적 일관성 + 채널별 정보 보존)
- **table encoding**으로 tabular 시계열을 텍스트 표현으로 변환 → LLM 의미 공간과 정렬
- table understanding 방식으로 MTSC를 재정식화 → task별 재학습 없이 분류
- **neighbor-assisted enhancement + multi-path reasoning**을 포함한 프롬프트로 LLM 추론 능력을 최대한 활용

### Contributions

1. MTSC를 위한 table understanding 패러다임을 제안하고, 이것이 기존 방법들의 병목을 완화하는 원리를 설명
2. 이 패러다임 하에서 LLM의 추론 능력을 활용하는 training-free 프레임워크 **TableTime** 설계
3. 10개 벤치마크 다변량 시계열 데이터셋에서 종합 실험을 수행해 table understanding 패러다임과 TableTime의 효과 검증


## 2 Related Work

### 2.1 Time Series Classification

시계열 분류 방법론의 발전 흐름을 정리:

1. **거리 기반(distance-based)**: DTW + K-NN — 시간적 왜곡(temporal distortion) 처리에는 효과적
2. **앙상블(ensemble)**: HIVE-COTE — 여러 feature transformation과 classifier를 계층적 투표(hierarchical voting)로 결합해 분류 성능 향상
3. **딥러닝 초기**: FCN(fully convolutional network), RNN — 원시 데이터에서 계층적 특징을 자동으로 학습, local/sequential dependency 포착에서 개선
4. **딥러닝 발전**: InceptionTime — multi-scale convolution을 활용한 더 깊은 네트워크로 다양한 시간 스케일의 복잡한 패턴 인식 능력 향상
5. **Transformer 기반**: long-range dependency와 global context 포착에 강점, 성능 한계를 계속 확장 중

### 2.2 LLMs in Time Series Analysis

LLM 기반 시계열 분석 접근을 두 갈래로 구분 (Intro의 prompt-based/retraining-based 구분과는 별개로, 여기서는 fine-tuning/generative modeling 축으로 재분류):

- **Fine-tuning 방법**: Linear Fine-Tuning 등 — 사전학습 LLM과 시계열 전용 encoder를 결합, LLM의 언어적 능력으로 패턴 식별
- **Generative modeling**: GPT 기반 forecasting(미래 시계열 시퀀스 예측), TEMPO(도메인 지식 통합)

#### LLM 기반 시계열 분석의 4가지 한계 (Intro의 4가지 병목과 거의 동일한 내용 재확인)

1. 시간적 의존성(temporal dependency) 및 채널별 특징 포착 어려움
2. 수치형 시계열 데이터와 LLM 의미 공간 간 불일치
3. 파인튜닝의 높은 계산 비용 (특히 대규모 적용 시)
4. LLM의 추론 능력을 충분히 활용하지 못함

→ 이 한계들을 해결하기 위해 table understanding 기반 패러다임인 **TableTime**을 제안한다는 흐름으로 Section 3(Preliminaries)·Section 4(The Proposed TableTime)로 연결됨.
