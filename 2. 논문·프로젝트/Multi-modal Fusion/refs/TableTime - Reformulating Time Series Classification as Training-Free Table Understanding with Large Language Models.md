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
updated: 2026-08-17
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


## 3 Preliminaries

### 3.1 Problem Definitions

**데이터셋 정의** (원문 수식):
$$\mathbb{D} = \{(X_1, y_1), (X_2, y_2), \dots, (X_n, y_n)\}$$
- $X_i \in \mathbb{R}^{t \times m}$: t개의 시간 스텝, m개의 feature(채널)를 갖는 다변량 시계열
- $y_i \in \{c_1, c_2, \dots, c_k\}$: k개 클래스 중 하나에 속하는 라벨

**분류 목표**: 입력 공간 X를 클래스 y에 대한 확률 분포로 매핑하는 분류기를 학습하는 것. (원문에는 이를 명시적인 f: X → y 형태의 수식으로는 제시하지 않고 서술로만 설명)

**TableTime의 정식화**: 일반적인 분류기 학습과 달리, TableTime은 파라미터 학습이 아니라 프롬프트를 통해 LLM에게 직접 텍스트를 생성시키는 방식으로 문제를 재정의함 (원문 수식):
$$T_i = \text{LLM}(P, X_i)$$
- P: 프롬프트, $X_i$: 입력 시계열
- $T_i$: LLM이 생성한 텍스트 응답 → 이후 정규표현식(regular expression)으로 $T_i$에서 예측 라벨 $\hat{y}_i$를 추출

즉 "학습된 파라미터로 예측"이 아니라 "프롬프트 입력 → 텍스트 생성 → 결과 파싱"이라는 training-free 흐름으로 MTSC를 재구성.

### 3.2 Large Language Models

LLM을 MTSC에 활용하는 근거로 4가지 장점을 제시:

1. **World Knowledge**: 다양한 도메인의 방대한 텍스트로 사전학습되어, 생성 결과에 일반 지식을 통합할 수 있음
2. **Reasoning**: 고급 추론·패턴 인식 능력을 보유 → 분류 정확도 향상에 기여할 잠재력
3. **Training-Free Inference**: 뛰어난 training-free 추론 능력을 보여줌 → task별 재학습 없이 도메인 간 일반화 가능
4. **Text Generation**: 텍스트 생성 패러다임으로 문제를 풂 → 해석 가능성(interpretability) 향상의 여지를 제공

→ 이 4가지 장점이 Section 1·2에서 언급된 LLM 기반 방법의 병목(수치-텍스트 의미 공간 불일치, 시간적/채널별 특징 포착 어려움, 파인튜닝 비용, 추론 능력 미활용)을 해소할 잠재력의 근거가 되며, Section 4의 TableTime 설계(tabular 변환 → table encoding → dual-driven reasoning)로 이어짐.


## 4 The Proposed TableTime

### 4.1 Model Architecture Overview

전체 파이프라인을 Figure 2로 개관하는 절. 원시 수치형 시계열이 입력되어 최종 라벨로 나오기까지의 흐름은 다음과 같은 순서로 진행됨:

1. **Neighbor Retrieval (이웃 검색)**: 테스트 샘플과 유사한(혹은 상이한) 학습 샘플들을 미리 찾아둠 → LLM이 태스크를 더 잘 이해하도록 돕는 참고 자료 역할
2. **Table Transformation (표 형식 변환)**: 원시 수치형 시계열을 tabular 형태로 변환 → 시간적 순서(temporal sequencing)와 채널별 정보(channel-specific information)를 모두 보존
3. **Prompt Construction (프롬프트 구성)**: 아래 3가지 요소를 통합한 프롬프트를 설계
   - **Context information**: 도메인 지식 등 모델을 방향 잡아주는 전문적 맥락 정보
   - **Neighbor knowledge**: 테스트 샘플을 유사/비유사 라벨을 가진 이웃 샘플들과 연결
   - **Task decomposition**: 단계별 추론을 유도하는 가이드
4. **LLM Reasoning**: 구성된 프롬프트를 바탕으로 tabular 표현 전체에 대해 LLM이 추론 수행
5. **Final Classification**: 추론 결과로부터 테스트 샘플의 최종 라벨 도출

즉 "원시 데이터 → 구조화된 변환(tabular) → 맥락·이웃 정보로 보강 → 가이드된 추론 → 라벨 결정"으로 이어지는 흐름이며, 이 과정 전체가 파라미터 학습 없이(training-free) 수행됨. 시간적 일관성과 채널 간 특징을 tabular 변환으로 보존한다는 점에서 Section 1·3에서 제시한 LLM 기반 MTSC의 요건들을 구조적으로 만족시키는 설계.

### 4.2 Context Information Modeling

#### 4.2.1 Reformulating Time Series as Tabular Data

**문제의식**: 기존 LLM 기반 모델은 시계열을 latent space에 직접 임베딩하거나 외부 모델 출력을 정렬하는 방식이라, temporal dependency와 channel relationship 정보가 손실되는 경우가 많음.

**해결 — table encoding**: 다변량 시계열을 아래와 같은 구조의 표로 재구성 (원문 수식):

![[Pasted image 20260817190316.png]]

```
      [ 0    Cᵀ  ]
X′ =  [          ]
      [ T    X   ]
```

- Cᵀ = (c₁, c₂, …, cₘ) — 채널(변수) 이름/정보
- T = (t₁, t₂, …, tₜ)ᵀ — 타임스탬프
- X — 원본 t×m 수치형 시계열

즉 첫 행에 채널명, 첫 열에 타임스탬프를 붙여 "행=시간, 열=채널"인 표 형태로 만듦 → 각 채널을 독립적으로 처리하면서도 순서 관계(sequential relationship)는 그대로 유지.

이 표는 다시 텍스트로 직렬화됨: **Text = Serialize(X′)** — DFLoader, Markdown 같은 serialization 방식으로 LLM이 읽을 수 있는 텍스트로 변환.

#### 4.2.2 Domain Context Information

LLM이 사전학습으로 방대한 지식을 갖고 있어도 프롬프트 설계에 민감하다는 점에 착안, tabular 표현 외에 **도메인 맥락 정보**를 추가로 제공. 3가지 구성 요소:

1. **Task definition**: 해당 도메인에서 분류 태스크가 무엇인지 간결하게 설명
2. **Dataset description**: 데이터의 구조·길이·특성에 대한 설명
3. **Class description**: 각 라벨의 정의와 범위

→ 모호성(ambiguity)을 줄이고, 모델의 추론을 태스크 제약에 맞게 정렬시키며, 출력의 일관성·신뢰성을 향상시킴.

### 4.3 Neighbor-Assisted In-Context Reasoner

**문제의식**: training-free MTSC에서는 모델이 테스트 샘플을 사전에 본 적이 없어 의미적 모호성(semantic ambiguity)이 발생 → temporal pattern에 대한 추론이 제한됨.

**해결**: retrieval-augmented 전략으로 의미적으로 관련된 학습 샘플을 찾아 "inductive cue"로 프롬프트에 삽입. **positive sample guidance**와 **contrast enhancement** 두 가지 전략을 함께 사용.

#### 4.3.1 Positive Sample Guidance

테스트 샘플마다 학습 데이터에서 k개의 최근접 이웃을 검색 (원문 수식):
![[Pasted image 20260818124208.png]]
N(X_test) = TopK(D_train, F_dist(X_test, X_i))

- TopK: 테스트 인스턴스와 거리가 가장 가까운 k개 샘플 선택
- F_dist: Euclidean distance 같은 거리 척도
- X_i: 개별 학습 샘플

→ 테스트 샘플과 유사한 temporal dynamics를 가진 예시를 모델에 제공.

#### 4.3.2 Contrast Enhancement

Positive 샘플뿐 아니라 클러스터링 기반으로 **negative 샘플**도 함께 제공:

1. **Clustering**: K-means로 학습 데이터를 클러스터 {Cₖ}로 분할
2. **Assignment**: 테스트 샘플을 가장 가까운 클러스터 중심에 할당
3. **Negative selection** (원문 수식): TopM(∪_{k≠j} C_k, F_dist(X_test, X_i))
   → 테스트 샘플이 속하지 않은 다른 클러스터들에서 거리가 가장 먼 M개 샘플 선택

→ "이 샘플이 무엇이 아닌지"를 함께 보여줌으로써 모델이 정답 방향으로 추론하도록 유도.

### 4.4 Task Decomposition Mechanism

**문제의식**: 기존 프롬프트는 복잡한 태스크에 대한 구조화된 가이드가 부족해, LLM이 각 샘플을 독립적으로(비일관적으로) 해석하게 됨.

**핵심 통찰**: 최근 연구에서 step-by-step reasoning이 LLM의 추론 능력을 유의미하게 향상시킨다는 것이 확인됨 → 이를 바탕으로 MTSC를 더 작은 순차적 단계들로 분해하는 task decomposition 도입.

**구현 (수작업 설계 대신 2단계 프로세스)**:
- **Stage 1 (Planning phase)**: 라벨이 있는 예시 하나를 **Planning LLM**에게 주고, 분류 과정을 단계별로 설명하도록 요청 → 이렇게 얻은 추론 경로를 일반화된 decomposition 템플릿으로 추상화
- **Stage 2 (Inference phase)**: 실제 분류 시에는 라벨에 접근하지 않는 별도의 **Reasoning LLM**이 이 구조화된 템플릿을 사용해 분류 수행 → 모델 내부 논리와의 정합성을 유지하면서도 training-free 조건을 보존

→ 복잡한 temporal pattern 분석·multi-channel feature extraction을 비구조적 해석 대신 체계적으로 다루게 함.

### 4.5 Multi-Path Ensemble Enhancement

**문제의식**: LLM 출력에는 본질적인 변동성(variability)이 존재.

**해결 — self-consistency**: 하나의 LLM에서 여러 출력을 얻어 가장 일관된 응답을 선택하는 방식으로 일관성·정확도를 향상.

**구현**: 서로 다른 LLM 파라미터(temperature) 집합 {T_i}(i=1..M)으로 동일 테스트 샘플에 대해 M번 추론을 수행. 각 설정 T_i에서의 예측은 f_{T_i}(X_test)로 표기.

**Aggregation — majority voting** (원문 수식): y_final = argmax_{y∈Y} Σ(i=1..M) 𝟙(f_{T_i}(X_test) = y_i)

**실험 설정**: 추론 경로 수 M=3, temperature는 각각 0.1 / 0.2 / 0.3으로 다양화.

→ 파라미터 다양성을 활용해 여러 그럴듯한 추론 경로를 샘플링함으로써, 단일 추론에서 오는 무작위성을 완화하고 robustness·accuracy를 향상.

### 4.6 Prompt Construction

최종 프롬프트는 앞서 다룬 3가지 요소를 통합한 구조:

1. **Domain context information**: task definition + dataset description + class definitions — 모델을 위한 일종의 "warm-up"
2. **Neighbor information**: 테스트 샘플을 유사/비유사 라벨을 가진 학습 샘플들과 연결
3. **Task decomposition**: 단계별 추론을 통해 최종 분류로 유도

Figure 3에서 이 3-파트 템플릿이 하나의 입력 구조로 어떻게 쌓이는지 시각화. 저자들은 "구조화된 프롬프트가 training-free 분류를 달성하는 데 핵심적"이라고 강조 — 명확한 지시가 없으면 LLM이 태스크 의도를 잘못 해석하거나 무관한 내용을 생성할 수 있음.

### 4.7 Remark and Discussion

기존 접근법 세 갈래와의 관계를 정리하며 TableTime의 위치를 설명:

1. **Table 기반 방법과의 관계**: 기존 tabular 모델은 handcrafted feature에 의존하지만, TableTime은 table을 semantic prompt로 사용 → 수작업 feature engineering 없이 temporal structure에 대해 직접 추론
2. **Distance 기반 방법과의 관계**: DTW 등 distance 기반 방법은 해석가능성(interpretability)은 있으나 noise에 민감; TableTime은 해석가능성을 유지하면서 LLM 기반 추론으로 robustness를 향상
3. **LLM 기반 방법과의 관계**: 기존 LLM 방법들은 외부 embedding이 필요해 계산 비용이 높지만, TableTime은 원시 시계열을 prompt-friendly한 table로 직접 인코딩 → representation loss 없이 training-free 분류를 지원

→ 결론적으로 TableTime은 **interpretability + robustness + efficiency**를 동시에 달성 — model-centric한 embedding 방식이 아니라 data-centric한 table understanding으로 이를 실현한다는 것이 핵심 주장.

