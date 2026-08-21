# MAPE-K 루프 (MAPE-K Loop)

## 한 줄 정의
시스템이 스스로 상황을 관찰하고, 분석하고, 계획하고, 실행하도록 만드는 **자가적응 시스템(Self-Adaptive System) 설계의 표준 참조 모델**.

## 기원
- **제안자/시기**: IBM, 2003~2004년경
- **제안 배경**: Kephart와 Chess가 IBM의 **자율 컴퓨팅(Autonomic Computing)** 이니셔티브의 핵심 구성요소로 제안함
- **문제의식**: 소프트웨어 시스템이 점점 복잡해지면서, 사람이 일일이 관리·튜닝하기 어려워짐 → 시스템이 사람처럼 "자율신경계"(autonomic)를 갖고 스스로 관리하게 만들자는 아이디어에서 출발
- 이후 자가적응 시스템(Self-Adaptive Systems, SAS) 연구 분야 전반에서 사실상의 표준(de facto standard) 참조 모델로 자리잡음

## 구성 요소 (5단계)

| 단계 | 이름 | 역할 |
|---|---|---|
| M | **Monitor** (관찰) | 센서를 통해 시스템 내부 상태 및 주변 환경 정보를 수집·전처리 |
| A | **Analyze** (분석) | 수집된 데이터를 평가하여 적응(변화)이 필요한지 판단 |
| P | **Plan** (계획) | 목표 상태에 도달하기 위한 구체적인 행동(들)을 결정 |
| E | **Execute** (실행) | 액추에이터를 통해 결정된 행동을 실제 시스템에 적용 |
| K | **Knowledge** (지식) | 위 4단계가 공통으로 참조·공유하는 지식 저장소 (모델, 규칙, 상태 정보 등) |

M-A-P-E 네 단계는 하나의 **피드백 루프(feedback loop)**를 형성하며, K는 이 루프 전체를 관통하며 데이터 공유·의사결정·통신을 지원한다.

## 핵심 개념: 자율 요소(Autonomic Element)

MAPE-K 루프를 갖춘 하나의 단위를 "자율 관리자(Autonomic Manager)"라고 부르며, 이것이 "관리 대상 시스템(Managed System/Element)"을 감시·제어하는 구조를 이룬다. 여러 개의 자율 요소를 계층적/병렬적/중첩적으로 조합하여 대규모 시스템을 구성할 수도 있다.

## 자율 컴퓨팅의 4가지 자가(Self-*) 속성

MAPE-K는 다음과 같은 자율 컴퓨팅의 목표 속성들을 실현하기 위한 구조로 설계되었다.

- **자가 구성(Self-Configuration)**: 변화하는 환경에서 자동으로 (재)구성
- **자가 최적화(Self-Optimization)**: 성능과 자원 효율을 지속적으로 개선
- **자가 치유(Self-Healing)**: 장애를 감지·진단·복구
- **자가 보호(Self-Protection)**: 악의적 공격이나 장애를 예측하고 방어

## 왜 널리 쓰이는가

- **모듈성**: 각 단계가 독립적인 책임을 가지므로, 특정 단계(예: Analyze)만 바꿔서 다른 알고리즘(예: 신경망)으로 대체하기 쉬움
- **범용성**: 클라우드 마이크로서비스, 로봇공학(ROS2), IoT, 엔터프라이즈 AI 에이전트 등 매우 다양한 도메인에 적용되어 옴
- **확장성**: 여러 MAPE-K 루프를 계층형(hierarchical) 또는 정보공유형(peer-to-peer) 패턴으로 연결해 대규모 분산 시스템 구성 가능

## 최근 동향

- 지식(Knowledge) 컴포넌트에 머신러닝을 결합하여 예측적/인과적 의사결정을 지원하는 방향으로 발전
- LLM 기반 에이전트(Agentic AI) 시스템에서도 MAPE-K 루프 구조를 자율적 판단-행동 사이클의 기본 틀로 채택하는 사례 증가

## 관련 문헌
- Kephart, J.O., Chess, D.M. (2003). *The Vision of Autonomic Computing*. IEEE Computer.
- IBM (2006). *An Architectural Blueprint for Autonomic Computing (ACRA)*.
- Weyns, D. (2020). *An Introduction to Self-Adaptive Systems: A Contemporary Software Engineering Perspective*.

## PANCS 논문과의 관계
PANCS 논문은 MAPE-K를 **그대로 재발명하지 않고**, 이 기존 표준 구조 위에 로봇 등 CPS 제어에 특화된 AMPC(적응형 모델 예측 제어)를 결합하여 구현한다. 즉, MAPE-K는 PANCS가 "빌려 쓰는 기존 골격"이며, PANCS의 독창성은 이 골격의 Analyze/Plan 단계를 AMPC 기반으로 구체화하고, 비선형 CPS 도메인에 맞게 각 하위 컴포넌트를 재사용 가능한 형태로 분해(decompose)했다는 데 있다.
