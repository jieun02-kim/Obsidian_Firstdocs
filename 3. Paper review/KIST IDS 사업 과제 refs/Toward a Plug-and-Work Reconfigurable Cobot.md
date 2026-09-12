---
type: literature
source: "Toward a Plug-and-Work Reconfigurable Cobot. IEEE/ASME Transactions on Mechatronics, 2022년 10월."
author: "Edoardo Romiti, Jörn Malzahn, Navvab Kashiri, Francesco Iacobelli, Marco Ruzzon, Arturo Laurenzi, Enrico Mingo Hoffman, Luca Muratore, Alessio Margan, Lorenzo Baccelliere, Stefano Cordasco, Nikos Tsagarakis"
year: 2022
venue: "IEEE/ASME Transactions on Mechatronics"
impact_factor: "확인 필요"
tags:
  - plug-and-work
  - cobot
  - reconfigurable-robot
  - modular-robot
  - EtherCAT
  - topology-recognition
  - urdf-generation
  - whole-body-control
project: "[[KIST IDS 사업 과제]]"
created: 2026-08-31
updated: 2026-09-10
---

## 개요
EtherCAT 기반 모듈형 협동로봇(cobot)을 재조립하면 (1) 토폴로지를 자동 인식하고, (2) 기구학·동역학 모델을 자동 생성해 URDF/SRDF로 저장하며, (3) 최적화 기반 컨트롤러를 재튜닝 없이 자동 재구성하는 완전한 HW+SW 아키텍처 제안("plug-and-work"). 4-DOF→5-DOF 재구성 실험으로 검증.

## Abstract (초록)
대량 생산에서 배치 사이즈가 단일 유닛 단위인 대량 맞춤화(mass-customization) 제품으로의 지속적인 추세는, 유지보수 다운타임이 짧고 적응성이 뛰어난 로봇 시스템의 필요성을 부각시켰습니다. 이러한 요구를 해결하기 위해, 본 연구에서는 빠르게 변화하는 유연한 제조 환경에서 많은 새로운 시나리오를 창출할 잠재력을 가진, 혁신적인 재구성 가능 협동 로봇(cobot) 개발을 제안합니다.

**기술적 기여**로서, 우리는 신속하게 재구성 가능한 EtherCAT 기반 로봇을 위한 완전한 하드웨어 및 소프트웨어 아키텍처를 제시합니다.
이 새로운 접근 방식은 각각이 EtherCAT 슬레이브를 나타내는 바디 모듈 세트로 구성된 다양한 로봇 구조의 토폴로지를 자동으로 재구성할 수 있게 합니다.
**이론적 기여**로서, 우리는 물리적 로봇이 조립되거나 재구성되는 즉시 로봇의 키네마틱(kinematic) 및 다이나믹(dynamic) 모델을 자동으로 획득하고 이를 URDF 형식으로 저장하는 방법을 제안합니다.
또한, 이 방법은 범용 최적화 기반 제어기를 자동으로 재설정하여 재구성 직후 즉시 사용할 수 있도록 합니다.

본 논문은 재구성 가능한 매니퓰레이터에 초점을 맞추고 있지만, 제안된 개념은 임의의 직렬 키네마틱 트리 구조 구성도 지원할 수 있습니다.

우리는 다음과 같은 사례를 통해 이러한 기여를 입증합니다:
(a) 로봇 토폴로지가 어떻게 재구성되고 URDF 모델이 생성되는지,
(b) 기본 모듈로 구축된 협동 로봇이 새로운 작업 공간 요구 사항을 충족하기 위해 4자유도(DOF) 로봇에서 5자유도(DOF) 로봇으로 신속하게 재구성되는 사례를 포함한 데카르트 작업(Cartesian task) 응용 프로그램.

## I. Introduction (서론)
- **배경**: 대량 맞춤 생산(mass customisation) 추세로 SME도 짧은 제품 수명주기·소량 배치에 대응할 로봇이 필요해졌지만, 기존 cobot은 SW만 유연하고 HW(자유도·기구학·페이로드)는 고정됨. 저자들은 "재구성에 걸리는 물리적 조립 시간"과 "재구성 후 재프로그래밍 시간"이 둘 다 짧아야 재구성 로봇의 유연성이 실질적 이점이 된다고 봄.
- **선행연구 흐름**: 80년대 말~90년대 초 초기 모듈형 매니퓰레이터 프로토타입 → 90년대 Chen의 자동 모델 생성 기법 → 2000년대 이후 탐사/우주/자기재구성/redundant 매니퓰레이터 등으로 확장 → 산업계(Schunk 모듈형 암 등)에도 등장.
- **저자들이 지적하는 공백**: 지금까지는 대부분 전자기계적 모듈 설계·모델링에 집중되어 있었고, 재구성 후 사용자가 **곧바로 프로그래밍·가동**할 수 있게 만드는 연구는 최근에야 소수 등장. 특히 [26][27](OIM/AIM)은 통신 네트워크에서 정보를 자동 추출하는 방법을 보이지 못했고, [28](ModMan)은 기구학만 재구성하고 동역학 기반 컨트롤러는 다루지 못함 — 자세한 비교는 아래 "인용 선행연구 비교" 참고.
- **핵심 기여 2가지**: (1) 4포트 EtherCAT 네트워크 구성을 활용한 자동 로봇 모델 탐지·생성 방법, (2) 로봇 구성과 무관하게 사용자 입력 없이 토크 제어 컴플라이언트 동작을 구현하는 컨트롤러 SW 아키텍처.

## II. Reconfiguration Process Overview (재구성 프로세스 개요, 5단계)
1. **모듈 장착/탈착**(유일한 수동 단계): 사용자가 원하는 기구학 구성이 되도록 모듈을 직접 연결
2. **네트워크 토폴로지 발견**: EtherCAT 통신이 수립되며 모듈 간 parent/child 관계를 자동 파악
3. **모듈 DB 조회**: 각 모듈이 가진 고유 식별자로 중앙 모듈 DB에서 파라미터를 가져옴
4. **물리적 로봇 토폴로지 재구성**: 기구학·동역학·의미정보(어떤 모듈이 end-effector인지 등)를 복원
5. **소프트웨어 모듈 재구성**: 미들웨어·컨트롤러가 새 토폴로지에 맞게 재구성되어 즉시 사용 가능

2~5단계는 완전 자동(on-the-fly)이며, 사용자 개입은 1단계(조립)뿐.

## III. Network Topology Recognition (네트워크 토폴로지 인식)
### 네트워크 기술 요구사항
제안 방법을 구현하기에 적합한 네트워크 기술은 다음 두 요구사항을 만족해야 함:
1. 각 슬레이브가 하나의 전자 장치로 구성되므로, 네트워크의 토폴로지는 슬레이브들을 체이닝(chaining)하여 트리형 로봇을 구성할 수 있어야 함. 이렇게 해야만 로봇 팔 같은 모듈형 **직렬** 기구학 로봇뿐 아니라, 다리 보행 플랫폼 같은 **트리형** 로봇도 설계할 수 있음.
2. 기구학·동역학 모델링을 위해서는 **정확한 네트워크 토폴로지를 추론**할 수 있어야 함 — 즉 슬레이브를 노드로, 슬레이브 간 연결을 엣지로 하는 그래프를 추출할 수 있어야 함.

이 두 요구사항을 만족하는 표준이 EtherCAT이며, 이하 내용은 이를 바탕으로 함.





### A. EtherCAT Networks (EtherCAT 네트워크)
- 각 모듈은 4-포트 EtherCAT Slave Controller(ESC) 칩을 하나 이상 내장한다고 가정. ESC는 EtherCAT 프로세서 유닛 + 최소 포트 0~2(선택적으로 포트 3)로 구성.
- 포트 0은 항상 마스터 방향을 향하는 **upstream 포트**. 마스터가 링에 삽입한 데이터 텔레그램은 포트 0으로 슬레이브에 도달 → 포트가 닫혀 있으면 다음 포트로 진행, 열려 있으면 연결된 슬레이브로 전달되었다가 되돌아와 다음 포트로 전달 → 최종적으로 마스터에 복귀.
- 각 포트는 해당 통신 링크가 활성/비활성화되면 자동으로 열리고 닫히며, 각 ESC는 마스터가 읽을 수 있는 포트 개폐 상태 레지스터를 가짐.

### B. Topology reconstruction algorithm (토폴로지 재구성 알고리즘)
- 네트워크는 슬레이브를 버스/트리/스타 형태의 **겉보기 토폴로지(apparent topology)로 연결할 수 있어 직렬·트리형 로봇을 구성할 수 있음. 하지만 EtherCAT의 실제(actual) 네트워크 토폴로지는 항상 하나의 열린 링**이며, ESC 내 포트 구성 차이만이 겉보기 토폴로지(=로봇의 물리적 형상)를 다르게 보이게 함.
- 이 때문에 서로 다른 두 물리적 로봇(Robot A/B 예시 — Torso 모듈이 각각 포트 0,1,3 / 0,1,2를 사용)이 네트워크 링 위에서는 **동일한 슬레이브 순서**로 나타날 수 있음. 이 겉보기 토폴로지 복원이 로봇 기구학·동역학 자동 복원의 첫 단계.
- 포트0=항상 upstream이라는 규약과, 마스터가 읽고 쓸 수 있는 ESC의 포트 개폐 레지스터를 이용해, 마스터는 링 위 모든 슬레이브를 순회하며 각 슬레이브의 parent(네트워크 링 상의 선행자이지만 반드시 직접 이웃은 아님)를 결정 가능 — Simple Open EtherCAT Master(SOEM)에 구현된 방식.
- 이 단계의 결과는 겉보기 네트워크 토폴로지를 나타내는 그래프 **χ**(슬레이브=노드, 포트 간 연결=엣지). 
  Chen[5]처럼 이 그래프도 AIM으로 더 압축된 형태로 표현 가능하나, 차이점은 관절을 포함한 **모든 종류의 모듈을 동등한 vertex로 취급**한다는 것.




## IV. Robot Physical Topology Recognition (로봇 물리적 토폴로지 인식)
그래프 χ의 각 노드에서 중앙 모듈 DB의 정보를 추출해, 물리 바디를 노드로 하는 트리형 데이터 구조 **φ**(관절·물리적 연결=엣지)로 집계. 모듈 종류: **Link/Joint 모듈**(포트 0·2 사용, 체인의 중간/끝), **End-Effector 모듈**(업스트림 포트 0만 사용, 체인 끝에만 위치), **Base 모듈**(모든 포트 사용 가능, EtherCAT 마스터·임베디드 PC 내장, 여러 브랜치로 분기 가능), **Hub 모듈**(마스터 없이 여러 브랜치 분기).


 URDF(Universal Robot Description Format) [30]
	 서로 다른 SW 에이전트 간 교환될 파일 형태

Featherstone [31] (Sec. IV-D)
	기구학 및 동역학 수량을 계산하는 로봇 모델



토폴로지의 구분 :
- Apparent Network Topology (외형적/논리적 네트워크 토폴로지)
	- 마스터가 EtherCAT 통신 데이터를 주고받는 과정에서 인식하는 **논리적인 연결 지도**
	- 모듈들이 통신상으로 어떤 순서로 연결되어 있고, 어떤 포트를 통해 데이터가 흐르는가를 나타냅
	- χ (Chi, 카이) 그래프 데이터 구조
- Physical Robot Topology (물리적 로봇 토폴로지)
	- 로봇이 실제로 어떻게 생겼는지(어떤 모듈이 몸체이고, 어디에 팔이 붙어 있는지)
	- ϕ (Phi, 파이) 트리 데이터 구조
	  바디 -> 노드
	  joints and physical connections -> edges
	  





### A. Module Database (모듈 데이터베이스)
χ를 생성한 후, 각 Slave에게 Slave 장치의 마이크로프로세서에 저장된 Module identifier를 요청

Module identifier
	중앙 집중식 모듈 데이터베이스에서 모듈 속성을 조회하기 위한 키(key) 역할. 4가지로 분류됨
- **Module type**: 다음과 같이 분류됩니다. 1은 능동형 Joint, 2는 Base, 3은 End-Effector, 4는 수동형 Link를 의미합니다.
- **Module id**: 동일한 유형의 모듈들을 구분하는 데 사용됩니다. 예를 들어, 직선형 Joint 모듈은 1, 엘보형 Joint 모듈은 2로 표시됩니다.
- **Module size**: 모듈의 크기를 나타내며, 1은 소형, 2는 중형, 3은 대형 모듈을 의미합니다.
- **Module revision number**: 모듈 설계의 후속 버전일수록 값이 증가합니다.

중앙 집중식 모듈 데이터베이스에 각 모듈 타입·버전별로 저장되는 속성은 최소한 다음을 포함:
- **좌표 변환(coordinate transformations)**: 모듈에 할당된 좌표계(coordinate frame)들 간의 변환
- **관성 파라미터(inertial parameters)**: 업스트림 프레임 기준 무게중심(CoM) 좌표, 모듈 질량, 무게중심 기준 관성 파라미터. Joint 모듈의 경우 업스트림 바디와 다운스트림 바디의 파라미터를 각각 별도로 저장
- **의미 정보(semantic information)**: 모듈의 공통 용도를 설명 — 예: End-effector 모듈을 'gripper', 'foot', 'wheel' 등으로 식별
- **제약(constraints) 파라미터**: 모듈과 연관된 기구학적·미분적·동역학적 제약 — 관절 가동 범위(motion range), 토크·속도 한계 등이 대표적
- **3D 메시 링크**: 모듈 바디를 그래픽으로 표현하는 3D 메시 파일 링크, 그리고 바디의 업스트림 프레임과 메시 원점 간 좌표 변환



- 각 모듈은 Module identifier(**type/id/size/revision** 4개 필드)를 가지며, 이를 키로 중앙 모듈 DB에서 좌표변환, 관성 파라미터, 의미정보(그리퍼/발/바퀴 등), 운동학적 제약(관절 가동범위·토크·속도 한계), 3D 메시 링크 등을 조회.




### B. Module Coordinate Frame Assignment (모듈 좌표계 할당)
자동 모델 생성을 정형화하기 위해 좌표계(coordinate frame) 규약을 도입.

**어디에 프레임을 두는가**
- **연결 인터페이스마다** 하나, **관절 축마다** 하나씩 프레임을 정의 — 이 프레임들이 모듈의 모든 기구학적(kinematic) 속성을 규정.
- 추가로 **움직이는 바디의 무게중심(CoM)마다** 하나의 레퍼런스 프레임을 둠(축은 업스트림 프레임과 평행) — 모듈의 관성적(inertial) 속성 위치를 지정.
- 이 프레임들 {f}과 그 사이의 상대 변환 T가 §IV-C에서 로봇을 URDF로 복원·기술하는 것을 가능케 함.

**표기법**
- 프레임 축은 X, Y, Z로 명명. 본 논문의 규약상 모듈 인터페이스의 **Z축은 항상 downstream 방향**을 가리킴.
- 접두사(leading subscript)는 특수 목적을 표시 — 예: 'j'는 그 프레임이 **관절의 동작 축(joint axis of action)**을 정의함을 뜻함. 접두사가 없으면 모듈의 (연결) 인터페이스 위치를 나타냄.
- 접미사 위첨자(trailing superscript)는 ESC의 인덱스/식별자, 접미사 아래첨자(trailing subscript)는 ESC의 포트 번호를 가리킴: `{purpose f^slave_id_port_id}` 형태로 표기.

![[Pasted image 20260911133711.png]]![[Pasted image 20260911133740.png]]


**정렬 원칙**
- 가능하면 좌표계를 **업스트림 프레임과 평행**하게 유지. 부득이 재정렬이 필요하면 **최소한의 축만 회전**시키는 방식을 취함.
- 연결된 EMI(Electro-Mechanical Interface) 양쪽의 두 프레임은 기본적으로 **일치(coincident)**하며, 공통 축을 중심으로 방향 오프셋 Ω를 가질 수 있음.
- 접두사 'j'로 표시된 관절 축의 경우, 동작 축은 항상 **Z축**.
- Link·End-Effector 모듈의 좌표계 할당은 비교적 단순(straightforward). 논문 Fig. 6의 Example I은 두 Joint 모듈이 연결될 때의 프레임 규약을, Example II는 Base 모듈에 적용된 프레임 규약을 보여줌 — 각 포트마다 EMI에 부착된 좌표계가 하나씩 존재함을 확인할 수 있음.

이 규약 덕분에 모듈 간 상대 기구학이 **오직 부모 모듈의 파라미터에만 의존**하도록 정형화됨(→ §IV-C의 변환행렬 T_λ(k),k 정의로 이어짐).


엔드 이펙터, 운동학적 체인 및 이를 구성하는 조인트에 대한 설명과 같은 로봇의 의미론적 정보
	URDF를 보완하기 위하여 -> MoveIt! 프레임워크 [33]에서 도입한 SRDF 파일(Semantic Robot Description Format)에 작성

URDF
	로봇의 질량, 관성, 링크 간의 연결 관계 등 기하학적이고 물리적인 모델링에 집중
**SRDF**
	로봇의 기능적인 부분, 즉 '이 로봇의 어느 부위가 엔드 이펙터인가?', '어떤 관절들이 하나의 운동학적 체인을 이루는가?'와 같은 정보를 정의.	시스템이 로봇을 더 똑똑하게 이해하도록 도움

### C. Modelling and URDF/SRDF Generation (모델링 및 URDF/SRDF 생성)
§IV-B에서 도입한 좌표계 규약은 로봇의 물리 모델을 **명확하게(unequivocally)** 도출할 수 있게 해줌. 짝지어진 연결 인터페이스에 결부된 기준 프레임은 서로 일치(coincident)하므로, 연속된 두 모듈 간 **상대 기구학은 오직 부모 모듈의 파라미터에만 의존**함.

**변환행렬 T_λ(k),k (식 1)**
- Featherstone[31]의 kinematic tree 표기법을 따라, 인덱스 k인 모듈의 부모를 λ(k)로 표기.
- 모듈 λ(k)와 k 사이의 변환행렬 T_λ(k),k는 두 모듈의 입력 포트 0에 연결된 프레임 {f^λ(k)_0}와 {f^k_0} 사이의 변환으로 정의:
  > T_λ(k),k = T_{f^λ(k)_0, f^k_0} = T_{f^λ(k)_0, f^λ(k)_pout} · T_{f^λ(k)_pout, f^k_0} = T^λ(k)_{0,pout}   ...(1)
  (마지막 항 T_{f^λ(k)_pout, f^k_0}은 두 EMI가 일치하므로 항등행렬 I이 되어 소거됨)
- 여기서 T^λ(k)_{0,pout} ∈ SE(3)이고, pout ∈ {0,1,2,3}는 다음 모듈이 연결된 (부모 모듈의) 출력 포트 번호. End-Effector 모듈일 때만 더미값 0을 가짐.
- 즉 그래프 χ의 임의 노드 k에 대한 변환은 **오직 부모 노드 λ(k)와 그 사이의 엣지(=pout 값을 내포)에만 의존** — 따라서 두 모듈 a, b 사이의 상대 순기구학은 그래프를 a에서부터 순회하며 식(1)을 b에 도달할 때까지 반복 호출해 계산 가능.

**모듈별 기구학 (식 2)**
- [5], [32] 같은 알고리즘으로 전체 순기구학 모델을 얻을 수 있음. 임의 모듈 k의 모듈러 기구학은 모듈 타입에 따라 다음과 같이 정의:
  > T^k_{0,pout} = T^k_{0,j} · e^(ŝ^k_j · q_k) · T^k_{j,pout},  (type = Joint)
  > T^k_{0,pout} = T^k_{0,pout},  (type = Link, Base)
  > T^k_{0,pout} = T^k_{0,tcp},  (type = End-Effector)   ...(2)
- 각 변환행렬의 의미: T^k_{0,j}는 {f^k_0}→{jf^k}(Joint 모듈의 **근위부(proximal)**), T^k_{j,pout}는 {jf^k}→{f^k_pout}(**원위부(distal)**), T^k_{0,pout}는 Link/Base 모듈의 입력포트(0)~출력포트 간, T^k_{0,tcp}는 End-Effector 모듈의 입력포트~TCP 간 변환.
- q_k는 모듈 k의 관절 변위. ŝ^k_j ∈ se(3)는 프레임 {f^k_j}에서 표현된 모듈 k 관절의 트위스트(twist). 트위스트 좌표를 나타내는 6차원 벡터 s^k_j는 상수이며, **회전(revolute) 관절**은 s^k_j = [0,0,0,0,0,1]ᵀ, **직동(prismatic) 관절**은 s^k_j = [0,0,1,0,0,0]ᵀ.

**그래프 φ 생성 및 URDF/SRDF 변환**
- 그래프 χ를 순회하며 각 노드에 식(2)와 DB에서 가져온 데이터를 적용해 확장 → 트리형 그래프 **φ**를 얻음. 예를 들어 Joint 모듈 노드 하나는 근위부·원위부 바디를 나타내는 두 노드로 확장되고, 그 사이는 구동되는 관절(actuated joint)을 나타내는 엣지로 연결됨. 노드는 각 움직이는 바디의 동역학 파라미터를, 엣지는 바디 간 변환을 저장 — 이는 OIM[26]이나 AIM[27]으로 더 압축된 형태로 변환 가능.
- ROS 기반 라이브러리의 사실상 표준(de-facto standard)인 **URDF**(XML 포맷)를 고려해, 그래프 φ를 URDF 파일로 변환 — 로봇을 일련의 **link 요소**(관성·시각·충돌 속성으로 구성)가 **fixed/prismatic/revolute joint 요소**로 연결된 형태로 표현. φ의 노드·엣지와 URDF XML 요소 사이의 매핑은 **1:1**.
- 두 링크 간(예: 연속된 두 Joint 모듈의 원위부-근위부) **정적인 물리적 연결**은 fixed joint 요소로 표현되며, 합성된 바디(composite body)의 동역학 파라미터 계산은 사용하는 동역학 라이브러리의 URDF 파서에 맡김.
- 로봇의 의미론적 정보(엔드 이펙터, 운동학적 체인 및 이를 구성하는 조인트에 대한 설명 등)는 URDF를 보완하기 위해 MoveIt! 프레임워크[33]가 도입한 **SRDF**(Semantic Robot Description Format) 파일에 별도로 작성.
  - **URDF**: 로봇의 질량, 관성, 링크 간 연결 관계 등 기하학적·물리적 모델링에 집중.
  - **SRDF**: '이 로봇의 어느 부위가 엔드 이펙터인가?', '어떤 관절들이 하나의 운동학적 체인을 이루는가?' 같은 기능적 정보를 정의 — 시스템이 로봇을 더 잘 이해하도록 도움.

### D. Kinematic and Dynamic Algorithms (기구학·동역학 알고리즘)
- 선택한 동역학 라이브러리는 URDF로부터 기구학·동역학 모델을 **명확하게(unequivocally)** 도출. 고빈도(high-frequency) 실시간 제어 루프 계산에 적합한, **spatial algebra 표기법**[31]을 사용하는 효율적인 라이브러리 구현체로 **KDL**[34], **Pinocchio**[35], **RBDL**[36]이 있음. 본 논문의 현재 구현은 RBDL을 사용했으나, 이 라이브러리들 모두 URDF 입력으로부터 주요 기구학·동역학 수치를 수치적으로 계산 가능.

- 구현된 강체 동역학(rigid body dynamics) 기술 알고리즘 3가지:
  - **역동역학(Inverse Dynamics) / Recursive Newton-Euler Algorithm (RNEA)**:
    > τ = RNEA(model, q, q̇, q̈) = M(q)q̈ + n(q, q̇)   ...(3)
  - **순동역학(Forward Dynamics) / Articulated Body Algorithm (ABA)**:
    > q̈ = ABA(model, q, q̇, τ)   ...(4)
  - **Composite Rigid Body Algorithm (CRBA)**:
    > M(q) = CRBA(model, q)   ...(5)
  - 여기서 model은 URDF를 파싱해 얻은 데이터 구조.
- 특히 §VI-C에서 구현한 컨트롤러에서는 **RNEA**로 Coriolis-원심력·중력 항 n을 계산하고, **CRBA**로 매니퓰레이터 질량행렬 M을 계산. 점 야코비안(point Jacobian), 가속도, 속도 등 다른 물리량도 [31]의 방식대로 모델 구조에서 계산 가능.





## V. Reconfigurable Software Architecture (재구성 가능한 소프트웨어 아키텍처)
하드웨어의 재구성 가능성을 활용하려면 SW도 새 토폴로지에 자동으로 적응해야 함 — 조립 직후 바로 가동 가능한 "plug-and-work" 시스템. 3계층 구조:

### A. Module Level (모듈 레벨)
- 각 HW 모듈의 펌웨어가 EtherCAT 네트워크 통신과 상태 측정 인터페이스 제공. 관절·바퀴 모듈 등 능동 모듈은 상위 레벨의 레퍼런스를 받아 구동하는 분산 제어기를 포함.

### B. Middleware Level (미들웨어 레벨)
- XBot(Muratore et al. 2020) 프레임워크 — 로보틱스 하드웨어의 다양성을 추상화하고 결정론적 hard RT 성능을 보장하는 플러그인 아키텍처. EtherCAT 마스터, RT 플러그인을 실행하는 **Plugin Handler**, non-RT 애플리케이션 레벨과의 통신을 담당하는 **Communication Handler**로 구성.
- URDF/SRDF만 있으면 매니퓰레이터든 휴머노이드든 사족보행이든 동일한 표준 API(XBotInterface)를 제공하고, 토폴로지가 바뀌면(예: 기구학 체인 추가) API도 자동으로 그에 맞게 바뀜.

### C. Application Level (애플리케이션 레벨)
- non-RT 스레드에서 실행되는 SW 레벨. ROS 프레임워크 인터페이스가 XBot에 내장되어 사용자·서드파티 ROS 노드와 통합 가능.
- CartesI/O 라이브러리가 Cartesian 공간 레퍼런스 궤적을 자동 생성하는 ROS API를 제공, XBot RT 플러그인 안에서 hard RT 제어 루프로 실행.
- 이 레벨의 재구성 가능성은 본질적(intrinsic) — 애플리케이션이 임의의 시점에 실행/종료되며 Communication Handler에 요청을 보내는 방식으로 하위 레벨과 상호작용.

## VI. Reconfigurable Centralized Control (재구성 가능한 중앙집중형 제어)
Interaction·force·impedance 등 안전 필수 중앙집중형 컨트롤러는 미들웨어의 RT 플러그인으로 실행되며, 로봇의 물리적 토폴로지가 바뀌어도 동역학적 한계를 지키며 안정적이어야 함 — 즉 제어 아키텍처에도 재구성 가능성이 필요.

### A. Optimisation-based Control (최적화 기반 제어)
- OpenSoT 라이브러리(QP 기반 **Stack of Tasks**)를 사용해 여러 태스크를 동시에 실행하고 복잡한 전신 동작을 구현. 태스크는 가중 최소자승 비용함수로, 제약은 선형 부등식으로 정식화. 태스크는 soft priority(비용함수 가중합)나 hard priority(널스페이스 투영 등)로 동시 실행 가능.

### B. Controller Reconfiguration Principle (컨트롤러 재구성 원리)
- 자유도가 추가/제거되면 제약 행렬의 열(column) 수만 바뀔 뿐 — **즉 컨트롤러 재구성은 수학적으로 비용함수·제약 행렬에 행/열을 추가·삭제하는 것과 동치**. OpenSoT가 자동 발견된 토폴로지와 사용자 정의 Stack of Tasks로부터 컨트롤러 수식을 자동 조립하므로, 모듈이 추가돼도 사용자가 태스크를 직접 갱신할 필요 없음(예: end-effector task frame이 새 위치로 자동 이동).

### C. Impedance Controller Implementation (임피던스 컨트롤러 구현)
- 시연에는 **Cartesian impedance controller**를 사용 — 목표 평형점으로부터의 편차에 대해 원하는 질량·감쇠·강성을 관계짓는 제어 법칙. QP 형태로 풀어 비선형 항을 보상.
- redundant 매니퓰레이터의 널스페이스는 postural task를 Stack of Tasks의 2순위로 추가해 처리. 핵심 주장: 모듈 추가/제거는 관련 행렬의 형태와 상태벡터 길이만 바꿀 뿐, **컨트롤러 구조 자체나 게인 재튜닝은 전혀 필요 없다.**

## VII. Experimental Results (실험 결과)
프로토타입: 직선/엘보 Joint 모듈, Base 모듈, Tool-exchanger End-Effector 모듈(마그네틱 툴 체인저). Joint는 Alberobotics 액추에이터(토크 센싱 내장) 사용. 기계적 연결은 C-couplings + 원뿔형 EMI(전기·통신·전원 겸용 커넥터, 볼트 2개로 체결, 최대 170 Nm 모멘트 견딤, 비숙련자도 1분 이내 연결 가능).

### A. Automatic discovery experiment (자동 발견 실험)
- 두 팔 로봇 모델을 조립 → EtherCAT 마스터가 겉보기 네트워크 토폴로지(χ) 자동 발견 → 모듈 DB 조회로 정보 집계 → 물리 토폴로지(φ) → URDF 생성 → 렌더링 검증. 모듈 조립부터 모델 자동 생성까지 평균 5분 이내.

### B. Cartesian task experiment (Cartesian 태스크 실험)
- 동일 드로잉(그림 그리기) 태스크를 4-DOF 로봇(가까운 종이)과 5-DOF 로봇(먼 종이, 모듈 하나 추가)으로 각각 수행. 빌드→자동발견→실행→(모듈 추가)적응→자동발견→재실행의 전체 사이클이 약 13분 만에 완료.
- 두 경우 모두 **동일한 강성·감쇠 게인**을 사용했음에도(재튜닝 없음) x-y 평면 추적 오차는 4-DOF 2.4mm, 5-DOF 3.3mm로 우수. 오차 증가분은 모듈 수 증가에 따른 누적 모델 오차로 추정, 추후 모듈별 파라미터 식별(identification)로 개선 여지.

## VIII. Conclusion (결론)
- 빌드 → 태스크 프로그래밍 → 실행 → (더 넓은 작업공간을 위한) 재구성 → 재실행까지의 전체 사이클을 약 13분 만에 시연 — 물리적 조립 시간과 재프로그래밍 시간이 동등하게 짧다는 저자들의 목표를 실증.
- 이는 (i) 잦은 제품 변화 대응, (ii) 유지보수 다운타임 최소화, (iii) 필요 시 새로운 로봇 설계를 즉석에서 조립하는 것을 가능케 함 — 로봇이 대량 맞춤 생산을 "돕는" 것을 넘어 로봇 자체가 "대량 맞춤 가능"해짐.
- **향후 연구**로 (1) 주어진 태스크 요구사항에 맞는 최적 로봇 구성을 사용자가 찾도록 돕는 SW 보조 도구, (2) floating-base 로봇(이동·보행·loco-manipulation)으로의 확장을 명시.

## 한계 (본 논문의 자체 언급을 넘어선 비판적 평가)
- 검증 범위가 **직렬 매니퓰레이터형 키네마틱 트리**에 한정됨. 논문 스스로도 "직렬 kinematic tree-like 구성을 지원한다"고 범위를 명시하는데, 실제 실증은 단일 팔(4→5 DOF)에 그쳐서 다리·팔·머리가 동시에 뻗어나가는 휴머노이드 같은 다중 분기(multi-branch) 구조에 그대로 스케일되는지는 검증되지 않음.
- 토폴로지 복원이 **순수하게 EtherCAT 네트워크 응답에만 의존**하는 결정론적 방식이라, 모듈이 정상 등록되어 응답한다는 전제가 깨지면(미등록 모듈, 통신 오류, 손상된 슬레이브) 대응 방법이 논문 범위 밖임. 또한 이 인식 방식은 **EtherCAT라는 특정 필드버스의 4-포트 ESC 구조**에 강하게 의존하므로, 다른 필드버스를 쓰는 모듈형 HW라면 알고리즘 자체는 재사용하기 어렵고 "포트 개폐 상태로 그래프를 복원한다"는 아이디어만 참고 가능.
- 이미지·시계열 등 **센서 기반 검증이 전혀 없음** — "네트워크가 이렇게 말했으니 이 토폴로지가 맞다"는 단일 소스 신뢰 구조이지, 여러 모달리티로 교차검증하는 구조가 아님.
- RT-safety(WCET, 락프리 캐시 등)에 대한 논의가 없음 — 산업용 협동로봇의 컨트롤 루프 재구성이 목표라, 휴머노이드 밸런싱 제어 수준의 hard real-time 요구사항까지 다루진 않음.

## KIST IDS 과제와의 연결점
- **명지대 담당 세부 주제**("자율 구성 모듈형 휴머노이드를 위한 신체 토폴로지 인식 및 실시간 제어 재구성 아키텍처 연구")의 목표와 문제 설정이 거의 그대로 겹치는 선행연구. 특히:
  - "모듈 metadata + device signal/status 기반 신체 topology·capability 자동 인식" ↔ 이 논문의 네트워크/물리 토폴로지 인식(EtherCAT 포트 상태 기반 + Module identifier로 중앙 DB 조회)
  - "실시간 제어 프레임워크에 반영 → 제어 가능 상태 진입, 동적 재구성" ↔ 이 논문의 XBot 미들웨어 API 자동 재구성 + OpenSoT 기반 컨트롤러의 행렬 크기 자동 재구성(재튜닝 불필요)
- 다만 위 "한계"에서 정리한 대로 EtherCAT 의존성, 단일 소스(네트워크) 신뢰 구조, RT-safety 미검토, Sim2Real·조작 지능(Task-level) 부재가 우리 과제와의 주요 차이점 — 세부과제3(SW 조작 지능)과의 접점은 약함.

## 인용 선행연구 비교 (References [22]–[28])
Introduction에서 "automated module discovery", "controller generation and tuning" 등 이 논문이 다루는 문제의 필요성을 뒷받침하며 인용하는 직접 선행연구 블록. 특히 [26][27]은 본 논문의 그래프 표현(χ, φ)이 잇는 이론적 계보이고, [28]은 본 논문이 스스로를 차별화하는 가장 직접적인 비교 대상.

| 번호 | 저자(연도) | 제목 | 유형 | 핵심 내용 | 본 논문과의 관계 |
|---|---|---|---|---|---|
| [22] | Baca, Woosley, Dasgupta, Nelson (2015) | [[Real-time distributed configuration discovery of modular self-reconfigurable robots]] | IEEE ICRA 학회논문 | 모듈형 자기재구성 로봇에서 실시간·분산(distributed) 방식으로 configuration을 탐지하는 기법 | "automated module discovery" 필요성의 근거로 인용. 본 논문처럼 특정 필드버스(EtherCAT) 기반이 아니라 범용 분산 알고리즘 관점 |
| [23] | V. Mayoral Vilches (2016) | [[Método de determinación de configuración de un robot modular]] (모듈형 로봇의 구성 결정 방법) | 스페인 특허 (ES 2661067B1) | 모듈형 로봇의 구성(configuration)을 판별하는 방법에 대한 특허 | 마찬가지로 "automated module discovery" 인용 목록에 포함 — 산업/특허 관점의 유사 시도 |
| [24] | Giusti & Althoff (2017) | [[On-the-Fly Control Design of Modular Robot Manipulators]] | IEEE Trans. Control Systems Technology | 모듈형 로봇 매니퓰레이터를 위한 즉석(on-the-fly) 제어기 설계 기법 | "automatic controller generation and tuning" 필요성의 근거로 인용 |
| [25] | Althoff, Giusti, Liu, Pereira (2019) | [[Effortless creation of safe robots from modules through self-programming and self-verification]] | Science Robotics | 모듈로부터 자가 프로그래밍(self-programming)·자가 검증(self-verification)을 통해 안전한 로봇을 손쉽게 만드는 프레임워크 | [24]와 같은 맥락("controller generation and tuning")으로 인용 — safety verification까지 포함한 더 포괄적인 접근이라는 점에서 대비됨 |
| [26] | Bi, Lin, Zhang (2010) | [[The general architecture of adaptive robotic systems for manufacturing applications]] | Robot. Comput. Integr. Manuf. | Axiomatic design을 적용해 재구성 로봇 시스템의 일반 아키텍처를 정의. Object Incidence Matrix(OIM) 도입 — 모듈별 기구학/동역학 파라미터를 담아 [27]의 AIM을 확장 | 본 논문이 직접 비교하는 선행연구 — "더 일반적인 모듈·연결 유형을 다룰 수 있게 확장"했다고 인정하면서도, "통신 네트워크로부터 이 정보를 자동으로 추출하는 방법은 보이지 않았다"는 것이 본 논문의 차별점 |
| [27] | I.-M. Chen (1994) | [[Theory and applications of modular reconfigurable robotic systems]] | 박사학위논문 (California Institute of Technology) | Assembly Incidence Matrix(AIM) 최초 도입 — 로봇 토폴로지를 행렬로 기술하는 이론적 틀 | [26]의 OIM이 확장한 원본 개념. 본 논문도 §IV-C에서 그래프 φ를 "OIM([26])이나 AIM([27])으로 더 압축된 형태로 표현 가능"하다고 언급하며 이 이론적 계보를 잇는다고 밝힘 |
| [28] | Yun, Moon, Ha, Kang, Lee (2020) | [[ModMan - An advanced reconfigurable manipulator system with genderless connector and automatic kinematic modeling algorithm\|ModMan: An advanced reconfigurable manipulator system with genderless connector and automatic kinematic modeling algorithm]] | IEEE Robotics and Automation Letters (RA-L) | 성별 없는(genderless) 커넥터 + 자동 기구학 모델링 알고리즘을 갖춘 재구성 매니퓰레이터 시스템 "ModMan" | **가장 직접적인 비교·차별화 대상.** 유사하게 기구학 구조를 자동 감지하지만 "(1) 재구성 프로세스의 시간 스케일(속도) 언급이 없고, (2) 기구학 모델만 재구성되어 동역학 기반 컨트롤러 구현이 불가능하다"고 명시 — 본 논문은 이 지점(속도 + 동역학 기반 토크 제어 재구성)을 자신의 기여로 내세움. 또한 §III-A 각주에서 genderless 커넥터를 이용해 포트 0의 연결을 하드웨어적으로 스왑하는 아이디어를 "[28]에서와 같이"라며 그대로 차용 |

## 메모
- 출처: [Toward a Plug-and-Work Reconfigurable Cobot | IEEE Xplore](https://ieeexplore.ieee.org/document/9550549/) (DOI: 10.1109/TMECH.2021.3106043)
- "인식 및 재구성 파트" 레퍼런스 — EtherCAT 기반 자동 토폴로지 인식 방식이 우리 과제의 "device signal/status 기반 신체 topology 자동 인식"과 가장 근접
- 다운로드한 PDF 파일명(`Towards a Plug-and-Work Reconfigurable Cobot.pdf`, `Z:\06_MEMBERS\02_JIEUNKIM\00_Projects\02_reconfiguration robot\`)은 저자 프리프린트/원고본으로 제목에 's'가 붙어 있으나, 공식 출판본(Crossref DOI 등록 제목 기준)과 동일 논문. 노트 파일명·링크는 공식 출판 제목("Toward", 's' 없음)을 기준으로 통일함.
- 관련 프로젝트 레퍼런스: [[An integrated system for perception-driven autonomy with modular robots]], [[Autonomous Self-Reconfiguration of Modular Robots by Evolving a Hierarchical Mechanochemical Model]]
