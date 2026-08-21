# Adaptive Model Predictive Control (AMPC)


## 참고자료
https://lsoovmee-rhino.tistory.com/entry/5


## 한 줄 정의
비선형 시스템의 동역학을 매 제어 주기마다 현재 동작점 주변에서 다시 선형화하여, 계산 효율성과 모델 정확도를 함께 확보하는 **모델 예측 제어(MPC)의 적응형(비선형 대응) 변형**.

## 상위 개념: MPC (Model Predictive Control)란?
AMPC를 이해하려면 먼저 MPC를 알아야 한다. MPC는 제어공학(control theory)에서 수십 년간 널리 쓰여온 기법으로, 공정 제어(화학 플랜트), 자율주행, 로봇 등에 광범위하게 적용된다.

**MPC의 동작 원리 (Receding Horizon 방식)**
1. 현재 시스템 상태에서, 앞으로 일정 구간(예측 호라이즌, horizon) 동안의 미래 거동을 예측
2. 목표(reference)와의 편차와 제어 노력을 최소화하는 **최적 제어 입력 시퀀스**를 계산 (제약조건 하의 최적화 문제 풀이)
3. 계산된 시퀀스 중 **첫 번째 제어 입력만 실제로 시스템에 적용**
4. 다음 시점에서 새로운 측정값을 받아 위 과정을 처음부터 반복 (호라이즌이 한 칸씩 미끄러지듯 이동 → "receding horizon")

## QP (Quadratic Program, 이차계획법)란?

**정의**: 목적함수(비용함수)가 변수들의 **이차식(quadratic)**이고, 제약조건은 전부 **선형(linear)**인 최적화 문제.

**일반형**
$$
\min_{x} \ \frac{1}{2}x^T H x + f^T x \quad \text{subject to} \quad Ax \le b
$$
- $x$: 최적화 대상 변수 (MPC에서는 미래 제어 입력 시퀀스)
- $H$: 이차항 계수 행렬 — **양의 준정부호(positive semi-definite)**면 문제가 볼록(convex)
- $Ax \le b$: 선형 부등식 제약 (예: 제어 입력 상·하한, 상태 상·하한)

**MPC의 비용함수가 왜 QP 형태가 되는가**
- MPC 비용함수 = (미래 상태 − 목표값)² + (제어 입력)² 형태 → 전형적인 이차식
- 시스템 모델이 선형이면, 이 비용함수를 제어 입력에 대해 전개해도 여전히 이차식으로 유지됨
- 제약(입력 한계, 상태 한계)도 선형 부등식 → 전체 문제가 QP로 정리됨

**QP가 "실시간으로 빠르게 풀린다"고 하는 이유**
- $H$가 양의 준정부호 → **볼록 최적화 문제** → 지역해(local optimum) = 전역해(global optimum), 해가 유일하게 보장됨
- Active-set method, interior-point method 등 성숙한 알고리즘과 전용 솔버(OSQP, qpOASES 등)가 있어 수 ms 단위로도 풀림
- 반대로 시스템이 비선형이면 문제가 **비볼록(non-convex)** 최적화가 되어(NMPC), 전역해 보장이 없고 계산량도 훨씬 커짐 — 이것이 NMPC가 실시간 제어에 부적합한 근본 이유이자, AMPC가 "매 스텝 선형화 → QP로 변환"하는 전략을 쓰는 이유

## MPC의 근본적인 문제: 비선형 시스템

일반적인(고전적인) MPC는 **선형(linear) 시스템 모델**을 전제로 하며, 이 경우 최적화 문제가 QP(Quadratic Program, 이차계획법)로 정리되어 실시간으로 빠르게 풀 수 있다.

그런데 로봇, 차량, 생체 시스템 등 실제 물리 시스템 대부분은 **비선형(nonlinear)**이다. 즉 입력과 출력이 단순 비례 관계가 아니다.
- 비선형 시스템을 그대로 최적화(Nonlinear MPC, NMPC)하면 **매우 무거운 비볼록(non-convex) 최적화 문제**가 되어 실시간(수십 ms 단위) 계산이 어려움
- 반대로 처음 한 번만 선형화해서 고정된 모델을 계속 쓰면, 시간이 지날수록 실제 상태와 모델이 어긋나(model mismatch) 예측이 부정확해짐

## AMPC의 해법: 연속적 재선형화 (Successive Linearization)

AMPC(혹은 SL-MPC, Successive Linearization MPC라고도 불림)는 이 딜레마를 다음과 같이 해결한다.

1. **매 제어 스텝마다**, 시스템의 비선형 모델을 **현재 관측된 동작점(operating point)** 주변에서 **야코비안(Jacobian) 기반으로 선형화**
2. 이 국소적인 선형 근사 모델을 이산화(discretize)하여, 그 스텝의 최적화 문제를 QP(이차계획법)로 변환 → 실시간으로 빠르게 풀 수 있게 됨
3. 다음 스텝이 되면 로봇은 이미 움직였으므로 동작점이 바뀌었고, 그 새로운 지점에서 **다시 선형화**를 수행
4. 이 과정을 반복 → "지금 이 순간에는 얼추 맞는" 선형 모델을 계속 새로 만들어가며 사용하는 셈

이렇게 하면 비선형 NMPC의 무거운 계산 부담 없이, 매 순간 실제 상태에 가깝게 맞춰진(적응된) 모델로 제어할 수 있다. "Adaptive"라는 이름이 붙는 이유가 바로 이 **매 순간 모델을 갱신(adapt)**하는 특성 때문이다.

## 자주 함께 쓰이는 보조 기법

- **칼만 필터(Kalman Filter) / EKF(Extended Kalman Filter)**: 센서 노이즈나 측정 불가능한 상태를 보정하기 위해, 재선형화된 모델과 함께 상태 추정을 실시간으로 업데이트하는 데 흔히 결합됨
- **Koopman 연산자 기반 방법**: 비선형 동역학을 고차원의 선형 함수 공간에 임베딩하여 다루는 데이터 기반 대안
- **Tube MPC / Robust MPC**: 선형화 오차를 "경계가 있는 외란(bounded disturbance)"으로 취급해 강건성을 확보하는 접근

## 장단점 요약

| 장점 | 단점 |
|---|---|
| 매 스텝 QP로 풀리므로 실시간 적용 가능 | 국소적(local) 근사이므로 예측 호라이즌이 길어질수록 오차 누적 |
| 비선형 시스템의 시변(time-varying) 특성에 지속 대응 | 정확한 비선형 모델(1차 원리 기반 모델)이 애초에 필요 (완전히 틀린 모델은 보정 불가) |
| 이미 검증된 QP 솔버·최적화 도구 재사용 가능 | 급격한 모드 전환(mode switching)이 있는 시스템에는 국소 선형화 가정이 깨질 수 있음 |

## 관련 문헌
- Adetola, V., DeHaan, D., Guay, M. (2009). *Adaptive model predictive control for constrained nonlinear systems*. Systems & Control Letters.
- Mayne, D.Q. et al. (2000). *Constrained model predictive control: Stability and optimality*. Automatica.
- 다수의 로봇·차량 응용 연구에서 "Successive Linearization MPC(SL-MPC)"라는 이름으로도 널리 다뤄짐

## PANCS 논문과의 관계
PANCS는 AMPC 자체를 새로 발명한 것이 아니라, 이미 제어공학 분야에서 확립된 **"매 스텝 재선형화 + QP 최적화"라는 기존 AMPC 기법**을 가져와 사용한다.

PANCS의 기여는:
- 이 AMPC를 **MAPE-K의 Analyze/Plan 단계 내부**에 하나의 소프트웨어 컴포넌트(`MgS. Linearization`, `Optimization`, `Prediction`, `Learning`)로 명시적으로 아키텍처화했다는 점
- 여기에 **칼만 필터 기반 학습(Learning)**을 결합해 모델-현실 불일치를 실시간 보정하고
- **Adaptive Config. Manager**를 통해 예측 호라이즌 길이 등을 실시간 자원 상황에 맞춰 동적으로 조절함으로써, 실시간 제약(real-time feasibility)까지 함께 보장하도록 설계했다는 점이다.
