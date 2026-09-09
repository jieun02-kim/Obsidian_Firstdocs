---
type: literature
source: Towards a Plug-and-Work Reconfigurable Cobot. IEEE/ASME Transactions on Mechatronics, 2022년 10월. (IEEE Xplore article 9550549 — 다운로드해 분석한 PDF 파일명은 'Towards...'(저자 프리프린트/원고본)이지만, 공식 발행 제목은 's' 없는 'Toward'가 맞음. 동일 논문)
author: Edoardo Romiti, Jörn Malzahn, Navvab Kashiri, Francesco Iacobelli, Marco Ruzzon, Arturo Laurenzi, Enrico Mingo Hoffman, Luca Muratore, Alessio Margan, Lorenzo Baccelliere, Stefano Cordasco, Nikos Tsagarakis
year: 2022
venue: IEEE/ASME Transactions on Mechatronics
impact_factor: 확인 필요
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
updated: 2026-09-08
---

## 핵심 요약
- **문제의식**: 대량 맞춤 생산(mass customisation) 추세로 SME도 짧은 제품 수명주기·소량 배치에 맞춰 빠르게 재구성 가능한 로봇이 필요해졌지만, 기존 협동로봇(cobot)은 SW 측면에서만 유연하고 HW(자유도·기구학·페이로드)는 고정되어 있음. 저자들은 "재구성에 걸리는 물리적 조립 시간"과 "재구성 후 다시 프로그래밍하는 시간"이 둘 다 똑같이 짧아야 재구성 로봇의 유연성이 실질적 이점이 된다고 봄.
- **핵심 기여**: EtherCAT 기반 모듈형 협동로봇을 위한 완전한 HW+SW 아키텍처를 제안. 로봇을 재조립하면 (1) 토폴로지를 자동으로 재구성하고, (2) 기구학·동역학 모델을 자동 생성해 URDF/SRDF로 저장하며, (3) 범용 최적화 기반 컨트롤러를 재구성 즉시 재사용 가능하도록 자동으로 재구성한다 — 사용자가 재구성 후 별도로 컨트롤러를 새로 짜거나 튜닝할 필요가 없음("plug-and-work").
- 논문은 직렬(serial) 매니퓰레이터 중심으로 시연하지만, 제안 개념 자체는 임의의 트리형(tree-like) 직렬 기구학 구성까지 지원 가능하다고 명시.
- 검증: 4자유도(4-DOF) 로봇을 5자유도(5-DOF)로 물리적 구조 변경 후, 모델 자동 생성 및 데카르트 좌표계 기반 작업(그림 그리기 태스크)이 재튜닝 없이 정상 동작함을 실증.

## 초록
대량 생산에서 배치 사이즈가 단일 유닛 단위인 대량 맞춤화(mass-customization) 제품으로의 지속적인 추세는, 유지보수 다운타임이 짧고 적응성이 뛰어난 로봇 시스템의 필요성을 부각시켰습니다. 이러한 요구를 해결하기 위해, 본 연구에서는 빠르게 변화하는 유연한 제조 환경에서 많은 새로운 시나리오를 창출할 잠재력을 가진, 혁신적인 재구성 가능 협동 로봇(cobot) 개발을 제안합니다.

**기술적 기여**로서, 우리는 신속하게 재구성 가능한 EtherCAT 기반 로봇을 위한 완전한 하드웨어 및 소프트웨어 아키텍처를 제시합니다. 
이 새로운 접근 방식은 각각이 EtherCAT 슬레이브를 나타내는 바디 모듈 세트로 구성된 다양한 로봇 구조의 토폴로지를 자동으로 재구성할 수 있게 합니다.
**이론적 기여**로서, 우리는 물리적 로봇이 조립되거나 재구성되는 즉시 로봇의 키네마틱(kinematic) 및 다이나믹(dynamic) 모델을 자동으로 획득하고 이를 URDF 형식으로 저장하는 방법을 제안합니다. 
또한, 이 방법은 범용 최적화 기반 제어기를 자동으로 재설정하여 재구성 직후 즉시 사용할 수 있도록 합니다. 

본 논문은 재구성 가능한 매니퓰레이터에 초점을 맞추고 있지만, 제안된 개념은 임의의 직렬 키네마틱 트리 구조 구성도 지원할 수 있습니다.

우리는 다음과 같은 사례를 통해 이러한 기여를 입증합니다: 
(a) 로봇 토폴로지가 어떻게 재구성되고 URDF 모델이 생성되는지, 
(b) 기본 모듈로 구축된 협동 로봇이 새로운 작업 공간 요구 사항을 충족하기 위해 4자유도(DOF) 로봇에서 5자유도(DOF) 로봇으로 신속하게 재구성되는 사례를 포함한 데카르트 작업(Cartesian task) 응용 프로그램.






## 재구성 프로세스 (5단계)
1. **모듈 장착/탈착**(유일한 수동 단계): 사용자가 원하는 기구학 구성이 되도록 모듈을 직접 연결
2. **네트워크 토폴로지 발견**: EtherCAT 통신이 수립되며 모듈 간 parent/child 관계를 자동 파악
3. **모듈 DB 조회**: 각 모듈이 가진 고유 식별자로 중앙 모듈 DB에서 파라미터를 가져옴
4. **물리적 로봇 토폴로지 재구성**: 기구학·동역학·의미정보(어떤 모듈이 end-effector인지 등)를 복원
5. **소프트웨어 모듈 재구성**: 미들웨어·컨트롤러가 새 토폴로지에 맞게 재구성되어 즉시 사용 가능

2~5단계는 완전 자동(on-the-fly)이며, 사용자 개입은 1단계(조립)뿐.

## 기술적 핵심 아이디어

### 1) EtherCAT 기반 네트워크 토폴로지 인식
- 각 모듈은 4-포트 EtherCAT Slave Controller(ESC) 칩을 하나 이상 내장. EtherCAT의 실제 네트워크 토폴로지는 항상 하나의 열린 링(open ring)이지만, 각 ESC의 포트 개폐(open/closed) 상태 조합에 따라 겉보기 토폴로지(apparent topology) — 즉 로봇의 실제 물리적 형상 — 가 달라짐.
- 포트 0은 항상 마스터 방향을 향하는 upstream 포트라는 규약과, 마스터가 읽을 수 있는 각 ESC의 포트 개폐 레지스터를 이용해, 네트워크 링을 순회하며 각 슬레이브의 parent를 결정 → 그래프 χ(슬레이브=노드, 포트 연결=엣지) 복원.
- 같은 네트워크 링 순서라도 서로 다른 물리적 로봇 토폴로지(Robot A/B 예시)를 나타낼 수 있다는 점이 이 문제의 핵심 난이도.

### 2) 물리적 토폴로지 인식 및 URDF/SRDF 자동 생성
- 각 모듈은 Module identifier(type/id/size/revision 4개 필드)를 가지며, 이를 키로 중앙 모듈 DB에서 좌표변환, 관성 파라미터, 의미정보(그리퍼/발/바퀴 등), 운동학적 제약(관절 가동범위·토크·속도 한계), 3D 메시 링크 등을 조회.
- 모듈 좌표계 규약(연결 인터페이스마다, 관절 축마다 좌표계 정의, Z축은 항상 downstream 방향)을 도입해 모듈 간 상대 기구학이 오직 부모 모듈의 파라미터에만 의존하도록 정형화 → 그래프 χ를 순회하며 Featherstone(2008)식 표기법으로 순기구학을 계산.
- 모듈 종류: Link/Joint 모듈(포트 0·2 사용, 체인의 중간/끝), End-Effector 모듈(업스트림 포트 0만 사용, 체인 끝에만 위치), Base 모듈(모든 포트 사용 가능, EtherCAT 마스터·임베디드 PC 내장, 여러 브랜치로 분기 가능), Hub 모듈(마스터 없이 여러 브랜치 분기).
- 최종적으로 그래프 φ(물리 바디=노드, 관절/물리적 연결=엣지)를 ROS 표준 포맷인 URDF로 1:1 매핑해 변환하고, end-effector·기구학 체인 등 의미정보는 MoveIt!의 SRDF로 저장. KDL/Pinocchio/RBDL 같은 spatial-algebra 기반 동역학 라이브러리(본 논문은 RBDL 사용)로 RNEA(역동역학)·ABA(순동역학)·CRBA(질량행렬) 계산.

### 3) 재구성 가능한 SW 아키텍처
3계층 구조:
- **모듈(펌웨어) 레벨**: 각 HW 모듈의 EtherCAT 통신·상태 측정·(관절 등 능동 모듈의) 분산 제어기
- **미들웨어 레벨**: XBot(Muratore et al. 2020) 프레임워크 — EtherCAT 마스터, RT 플러그인을 실행하는 Plugin Handler, non-RT 애플리케이션 레벨과의 통신을 담당하는 Communication Handler로 구성. URDF/SRDF만 있으면 매니퓰레이터든 휴머노이드든 사족보행이든 동일한 표준 API를 제공하고, 토폴로지가 바뀌면 API도 자동으로 그에 맞게 바뀜.
- **애플리케이션 레벨**: non-RT 스레드에서 실행되는 ROS 연동 SW. CartesI/O 라이브러리가 Cartesian 공간 목표 궤적을 자동 생성해 RT 제어 루프로 전달.

### 4) 재구성 가능한 중앙집중형 제어기 (컨트롤러 자동 재형성)
- OpenSoT 라이브러리(QP 기반 Stack of Tasks)를 사용. 각 태스크는 가중 최소자승 비용함수, 제약은 선형 부등식으로 정식화되며, 자유도가 추가/제거되면 이 행렬들의 열(column) 수만 바뀔 뿐 — **즉 재구성은 수학적으로 비용함수·제약 행렬에 행/열을 추가·삭제하는 것과 동치**이며, OpenSoT가 자동 발견된 토폴로지와 사용자 정의 Stack of Tasks로부터 컨트롤러 수식을 자동 조립.
- 시연에는 Cartesian impedance controller를 사용. redundant 매니퓰레이터의 널스페이스는 postural task를 2순위로 추가해 처리. 핵심 주장: 모듈 추가/제거는 상태벡터 길이와 관련 행렬의 형태만 바꿀 뿐, **컨트롤러 구조 자체나 게인 재튜닝은 전혀 필요 없다.**

## 실험
- 프로토타입: 직선/엘보 Joint 모듈, Base 모듈, Tool-exchanger End-Effector 모듈(마그네틱 툴 체인저). Joint는 Alberobotics 액추에이터(토크 센싱 내장) 사용. 기계적 연결은 C-couplings + 원뿔형 EMI(전기·통신·전원 겸용 커넥터, 볼트 2개로 체결, 최대 170 Nm 모멘트 견딤, 비숙련자도 1분 이내 연결 가능).
- **자동 발견 실험**: 두 팔 로봇 모델을 조립 → EtherCAT 마스터가 겉보기 네트워크 토폴로지(χ) 자동 발견 → 모듈 DB 조회로 정보 집계 → 물리 토폴로지(φ) → URDF 생성 → 렌더링 검증. 모듈 조립부터 모델 자동 생성까지 평균 5분 이내.
- **Cartesian task 실험**: 동일 드로잉(그림 그리기) 태스크를 4-DOF 로봇(가까운 종이)과 5-DOF 로봇(먼 종이, 모듈 하나 추가)으로 각각 수행. 빌드→자동발견→실행→(모듈 추가)적응→자동발견→재실행의 전체 사이클이 약 13분 만에 완료. 두 경우 모두 **동일한 강성·감쇠 게인**을 사용했음에도(재튜닝 없음) x-y 평면 추적 오차는 4-DOF 2.4mm, 5-DOF 3.3mm로 우수. 오차 증가분은 모듈 수 증가에 따른 누적 모델 오차로 추정, 추후 모듈별 파라미터 식별(identification)로 개선 여지.

## 한계
- 검증 범위가 **직렬 매니퓰레이터형 키네마틱 트리**에 한정됨. 논문 스스로도 "직렬 kinematic tree-like 구성을 지원한다"고 범위를 명시하는데, 실제 실증은 단일 팔(4→5 DOF)에 그쳐서 다리·팔·머리가 동시에 뻗어나가는 휴머노이드 같은 다중 분기(multi-branch) 구조에 그대로 스케일되는지는 검증되지 않음. 논문도 floating-base 로봇(이동·보행·loco-manipulation)으로의 확장을 향후 과제로 명시.
- 토폴로지 복원이 **순수하게 EtherCAT 네트워크 응답에만 의존**하는 결정론적 방식이라, 모듈이 정상 등록되어 응답한다는 전제가 깨지면(미등록 모듈, 통신 오류, 손상된 슬레이브) 대응 방법이 논문 범위 밖임. 또한 이 인식 방식은 **EtherCAT라는 특정 필드버스의 4-포트 ESC 구조**에 강하게 의존하므로, 다른 필드버스를 쓰는 모듈형 HW라면 알고리즘 자체는 재사용하기 어렵고 "포트 개폐 상태로 그래프를 복원한다"는 아이디어만 참고 가능.
- 이미지·시계열 등 **센서 기반 검증이 전혀 없음** — "네트워크가 이렇게 말했으니 이 토폴로지가 맞다"는 단일 소스 신뢰 구조이지, 여러 모달리티로 교차검증하는 구조가 아님.
- RT-safety(WCET, 락프리 캐시 등)에 대한 논의가 없음 — 산업용 협동로봇의 컨트롤 루프 재구성이 목표라, 휴머노이드 밸런싱 제어 수준의 hard real-time 요구사항까지 다루진 않음.
- 주어진 태스크 요구사항에 맞는 최적 로봇 구성을 사용자가 찾도록 돕는 SW 보조 도구 개발도 향후 과제로 남겨둠. Impedance 제어의 컴플라이언스 특성을 희생하지 않으면서 추적 성능을 높이는 다른 제어기 확장 가능성도 언급.

## KIST IDS 과제와의 연결점
- **명지대 담당 세부 주제**("자율 구성 모듈형 휴머노이드를 위한 신체 토폴로지 인식 및 실시간 제어 재구성 아키텍처 연구")의 목표와 문제 설정이 거의 그대로 겹치는 선행연구. 특히:
  - "모듈 metadata + device signal/status 기반 신체 topology·capability 자동 인식" ↔ 이 논문의 네트워크/물리 토폴로지 인식(EtherCAT 포트 상태 기반 + Module identifier로 중앙 DB 조회)
  - "실시간 제어 프레임워크에 반영 → 제어 가능 상태 진입, 동적 재구성" ↔ 이 논문의 XBot 미들웨어 API 자동 재구성 + OpenSoT 기반 컨트롤러의 행렬 크기 자동 재구성(재튜닝 불필요)
- 다만 위 "한계"에서 정리한 대로 EtherCAT 의존성, 단일 소스(네트워크) 신뢰 구조, RT-safety 미검토, Sim2Real·조작 지능(Task-level) 부재가 우리 과제와의 주요 차이점 — 세부과제3(SW 조작 지능)과의 접점은 약함.

## 인용 선행연구 비교 (References [22]–[28])
Introduction에서 "automated module discovery", "controller generation and tuning" 등 이 논문이 다루는 문제의 필요성을 뒷받침하며 인용하는 직접 선행연구 블록. 특히 [26][27]은 본 논문의 그래프 표현(χ, φ)이 잇는 이론적 계보이고, [28]은 본 논문이 스스로를 차별화하는 가장 직접적인 비교 대상.

| 번호   | 저자(연도)                                 | 제목                                                                                                                         | 유형                                          | 핵심 내용                                                                                                               | 본 논문과의 관계                                                                                                                                                                                                                                                           |
| ---- | -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [22] | Baca, Woosley, Dasgupta, Nelson (2015) | [[Real-time distributed configuration discovery of modular self-reconfigurable robots]]                                        | IEEE ICRA 학회논문                              | 모듈형 자기재구성 로봇에서 실시간·분산(distributed) 방식으로 configuration을 탐지하는 기법                                                      | "automated module discovery" 필요성의 근거로 인용. 본 논문처럼 특정 필드버스(EtherCAT) 기반이 아니라 범용 분산 알고리즘 관점                                                                                                                                                                            |
| [23] | V. Mayoral Vilches (2016)              | [[Método de determinación de configuración de un robot modular]] (모듈형 로봇의 구성 결정 방법)                                            | 스페인 특허 (ES 2661067B1)                       | 모듈형 로봇의 구성(configuration)을 판별하는 방법에 대한 특허                                                                           | 마찬가지로 "automated module discovery" 인용 목록에 포함 — 산업/특허 관점의 유사 시도                                                                                                                                                                                                      |
| [24] | Giusti & Althoff (2017)                | [[On-the-Fly Control Design of Modular Robot Manipulators]]                                                                    | IEEE Trans. Control Systems Technology      | 모듈형 로봇 매니퓰레이터를 위한 즉석(on-the-fly) 제어기 설계 기법                                                                          | "automatic controller generation and tuning" 필요성의 근거로 인용                                                                                                                                                                                                            |
| [25] | Althoff, Giusti, Liu, Pereira (2019)   | [[Effortless creation of safe robots from modules through self-programming and self-verification]]                             | Science Robotics                            | 모듈로부터 자가 프로그래밍(self-programming)·자가 검증(self-verification)을 통해 안전한 로봇을 손쉽게 만드는 프레임워크                                 | [24]와 같은 맥락("controller generation and tuning")으로 인용 — safety verification까지 포함한 더 포괄적인 접근이라는 점에서 대비됨                                                                                                                                                               |
| [26] | Bi, Lin, Zhang (2010)                  | [[The general architecture of adaptive robotic systems for manufacturing applications]]                                        | Robot. Comput. Integr. Manuf.               | Axiomatic design을 적용해 재구성 로봇 시스템의 일반 아키텍처를 정의. Object Incidence Matrix(OIM) 도입 — 모듈별 기구학/동역학 파라미터를 담아 [27]의 AIM을 확장 | 본 논문이 직접 비교하는 선행연구 — "더 일반적인 모듈·연결 유형을 다룰 수 있게 확장"했다고 인정하면서도, "통신 네트워크로부터 이 정보를 자동으로 추출하는 방법은 보이지 않았다"는 것이 본 논문의 차별점                                                                                                                                                |
| [27] | I.-M. Chen (1994)                      | [[Theory and applications of modular reconfigurable robotic systems]]                                                          | 박사학위논문 (California Institute of Technology) | Assembly Incidence Matrix(AIM) 최초 도입 — 로봇 토폴로지를 행렬로 기술하는 이론적 틀                                                      | [26]의 OIM이 확장한 원본 개념. 본 논문도 §IV-C에서 그래프 φ를 "OIM([26])이나 AIM([27])으로 더 압축된 형태로 표현 가능"하다고 언급하며 이 이론적 계보를 잇는다고 밝힘                                                                                                                                                      |
| [28] | Yun, Moon, Ha, Kang, Lee (2020)        | [[ModMan - An advanced reconfigurable manipulator system with genderless connector and automatic kinematic modeling algorithm\|ModMan: An advanced reconfigurable manipulator system with genderless connector and automatic kinematic modeling algorithm]] | IEEE Robotics and Automation Letters (RA-L) | 성별 없는(genderless) 커넥터 + 자동 기구학 모델링 알고리즘을 갖춘 재구성 매니퓰레이터 시스템 "ModMan"                                                 | **가장 직접적인 비교·차별화 대상.** 유사하게 기구학 구조를 자동 감지하지만 "(1) 재구성 프로세스의 시간 스케일(속도) 언급이 없고, (2) 기구학 모델만 재구성되어 동역학 기반 컨트롤러 구현이 불가능하다"고 명시 — 본 논문은 이 지점(속도 + 동역학 기반 토크 제어 재구성)을 자신의 기여로 내세움. 또한 §III-A 각주에서 genderless 커넥터를 이용해 포트 0의 연결을 하드웨어적으로 스왑하는 아이디어를 "[28]에서와 같이"라며 그대로 차용 |

## 메모
- 출처: [Toward a Plug-and-Work Reconfigurable Cobot | IEEE Xplore](https://ieeexplore.ieee.org/document/9550549/)
- "인식 및 재구성 파트" 레퍼런스 — EtherCAT 기반 자동 토폴로지 인식 방식이 우리 과제의 "device signal/status 기반 신체 topology 자동 인식"과 가장 근접
- 다운로드한 PDF 파일명(`Towards a Plug-and-Work Reconfigurable Cobot.pdf`, `Z:\06_MEMBERS\02_JIEUNKIM\00_Projects\02_reconfiguration robot\`)은 저자 프리프린트/원고본으로 제목에 's'가 붙어 있으나, 공식 출판본과 동일 논문. 노트 파일명·링크는 공식 출판 제목("Toward", 's' 없음)을 기준으로 통일함.
- 관련 프로젝트 레퍼런스: [[An integrated system for perception-driven autonomy with modular robots]], [[Autonomous Self-Reconfiguration of Modular Robots by Evolving a Hierarchical Mechanochemical Model]]
