# TwinCAT

## 핵심 요약
- TwinCAT = 범용 PC를 실시간 PLC/모션 제어기로 바꾸는 Beckhoff(독일)社의 통합 소프트웨어
- 정식 명칭: The Windows Control and Automation Technology
- 핵심 경쟁력: Windows 위에 얹은 전용 Real-Time Kernel(μs 단위 주기) + Visual Studio 기반 통합 개발환경
- EtherCAT 마스터 기능까지 내장 — ESI 매핑, PDO/SDO 통신을 TwinCAT 하나로 총괄

---

## 핵심 역할
- **PC 기반 제어기 변환**: 전용 PLC 하드웨어 대신 범용 PC CPU 자원으로 실시간 제어 환경 구축
- **실시간(Real-Time) OS 구현**: Windows 하단에 전용 Real-Time Kernel 레이어 배치 → 일반 OS의 지연 없이 1ms 이하(μs 단위) 주기 제어 보장
- **통합 자동화 플랫폼**: PLC 개발, HMI 디자인, 서보 드라이브 모션 제어, C/C++ 연동, AI/C# 통합 개발환경을 Visual Studio 기반 한 곳에서 제공

---

## 주요 기능

### IEC 61131-3 표준 PLC 언어
- **ST** (Structured Text)
- **LD** (Ladder Diagram)
- **FBD** (Function Block Diagram)

### 모션 제어 (TwinCAT NC / CNC)
- 서보 드라이브 위치·속도·토크 제어
- 동기 제어: 가상 축, 전자 캠, 보간 제어

### EtherCAT 마스터(Master) 기능
- 버스 스캔
- ESI 파일 읽기/매핑
- 초고속 이더넷 주기 통신(PDO/SDO) 총괄 관리

### C/C++ 및 MATLAB/Simulink 연동
- 고난도 제어 알고리즘·수치 모델을 C/C++ 또는 MATLAB에서 빌드 → 실시간 커널 모듈로 직접 탑재

### 통합 엔지니어링 환경 (TwinCAT XAE)
- Microsoft Visual Studio 프레임워크에 완전 통합
- 개발·디버깅·네트워크 진단·모니터링을 한 화면에서 처리
