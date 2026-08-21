# ESI / EDS 

## 핵심 요약
- ESI·EDS 둘 다 "장치 설명서" 역할 — 상위 제어기(마스터)가 슬레이브 장치를 인식·등록하도록 도움
- 구분은 통신 프로토콜 기준: **ESI = EtherCAT**, **EDS = CANopen / EtherNet/IP**

---

## ESI (EtherCAT Slave Information)

### 정의
- EtherCAT 슬레이브(서보 드라이브 등)의 하드웨어 특성·통신 매개변수를 정의하는 XML 기반 구성 파일
- EtherCAT 마스터가 드라이브를 인식·제어하도록 돕는 장치 설명서

### 주요 역할
- **장치 식별**: 제조사 정보, 제품 코드, 시리얼 번호, 지원 통신 속도
- **데이터 매핑**: 입출력 데이터 구조(PDO), 파라미터 구조(SDO)
- **상위 제어기 등록**: TwinCAT, CoDeSys 등에 Import → 드라이브 네트워크 등록

### 등록 시 가능해지는 것
- **장치 자동 인식**: 모델명·제조사·제어 규격 자동 등록
- **통신 데이터 연결**: 위치/속도/토크/에러 상태 등 PDO/SDO ↔ 제어 프로그램 변수 즉시 연결
- **복잡한 통신 설정 생략**: 통신 주기·매개변수 직접 코딩 불필요, 바로 제어 로직 작성 가능

---

## ESI 규격 (ETG.2000)

### 표준
- ETG(EtherCAT Technology Group) 공식 명세 **ETG.2000** (EtherCAT Slave Information Specification)
- XML Schema(`EtherCATInfo.xsd`) 기반 — 마스터가 로드 시 구문 오류·필수 태그 누락 검증

### 주요 구성 태그
|태그|내용|
|---|---|
|`<Vendor>`|제조사 ID, 이름|
|`<Descriptions>` → `<Devices>`|장치 ID, 프로필(CoE/SoE 등), PDO 크기, SDO dictionary|
|`<Mailbox>`|통신 프로토콜(CoE, FoE, EoE 등) 지원 여부|

### 마스터 연동 3단계
1. **데이터베이스 등록 (Parsing & Database)**: 마스터가 시작 시 지정 ESI 폴더 파싱 → 내부 Device Library 구축
2. **장치 매칭 및 ENI 생성 (Scanning & Config)**: 버스 스캔 → 드라이브 EEPROM의 Vendor ID / Product Code / Revision Number 읽음 → ESI DB와 대조·매핑 → ENI(ETG.2100) 생성
3. **Run-time 통신 설정 (Initialization)**: ENI 기반으로 Init → Pre-Op → Safe-Op → Op 전이하며 Sync Manager, FMMU, PDO/SDO 설정을 슬레이브에 주입

---

## EDS (Electronic Data Sheet)
- CANopen / EtherNet/IP 네트워크용 장치 정보 파일 (텍스트/XML)
- 파라미터 목록, 통신 규격 등을 담음
- ESI와 유사한 역할 — 마스터가 장치와 통신하도록 규격을 등록하는 "장치 명세서"
