
# EtherCAT 상태 점검 - 2 Layer 구조

## 핵심 요약

- Layer 1(AL+WKC) 통과 = 통신 신뢰 가능 전제조건, 모든 슬레이브 공통
- Layer 2(CiA402) = 서보 드라이브 전용, 실제 제어 가능 여부 판단
- 순서: **Layer 1 확인 → 통과 시에만 Layer 2 판단 진입** (CiA402 상태머신만으로는 판단 불가)
- RAON-RT의 SlaveKistFT.h가 "Layer 2 없이 바로 데이터 처리"하는 대표 케이스

---

## Layer 1: EtherCAT AL 상태 (통신 계층)
Application Layer

### 담당 범위

- 마스터-슬레이브 간 데이터 교환 가능 여부만 다룸
- 모터/센서 등 슬레이브 종류 무관, **모든 슬레이브 예외 없이 거침**
- ESC(EtherCAT Slave Controller) 하드웨어 레벨 상태

![[Pasted image 20260811061657.png]]

### 4단계 전이
- INIT: initialization, 통신 없음, EEPROM emulation 활성화
- PRE-OP: mailbox 활성화, 슬레이브 parameterization 및 startup parameter 처리
- SAFE-OP: cyclical actual value 전송, 드라이브 동기화 시도
- OPERATIONAL: cyclical setpoint 처리, torque enable 활성화 가능, 드라이브 동기화 필수

- INIT: 메일박스만 가능
- PREOP: SDO 통신 가능, PDO 불가
- SAFEOP: TxPDO(입력)만 유효, RxPDO(출력) 미반영
- OP: PDO 입출력 전부 사이클릭 정상 교환

### IgH 체크 항목

- `ecrt_master_state()` → link_up, slaves_responding, al_states
- `ecrt_domain_state()` → working_counter, wc_state == EC_WC_COMPLETE
- WKC 불일치 = 슬레이브 무응답 = 해당 사이클 PDO값 신뢰 불가

```c
ecrt_domain_process(domain);
ecrt_domain_state(domain, &ds);
if (ds.wc_state != EC_WC_COMPLETE) {
    // Layer 2 로직 진입 자체를 스킵, safe state 유지
}
```

---

## Layer 2: CiA402 상태머신 (응용 계층)

### 담당 범위

- 서보 드라이브가 실제 토크/위치 제어 가능한지 판단
- **CiA402 프로파일 따르는 슬레이브만 해당** (서보 드라이브 등)
- 드라이브 내부 펌웨어가 관리, 마스터는 Controlword로 "요청"만 가능
![[Pasted image 20260811061621.png]]


### 상태 전이

```
Not Ready to Switch On
   ↓ (자동)
Switch On Disabled
   ↓ Shutdown (CW=0x06)
Ready to Switch On
   ↓ Switch On (CW=0x07)
Switched On
   ↓ Enable Operation (CW=0x0F)
Operation Enabled  ← 실제 제어 가능 지점
```

### Controlword 명령

|명령|값|비고|
|---|---|---|
|Shutdown|0x06|Ready to Switch On 요청|
|Switch On|0x07|Switched On 요청|
|Enable Operation|0x0F|Operation Enabled 요청|
|Disable Voltage|0x00|강제 전원 차단|
|Quick Stop|0x02|비상 정지 시퀀스|
|Fault Reset|0x80 (rising edge)|Fault 복구, 엣지 트리거 필요|

### Statusword 판별 (mask 0x6F)

|값|상태|
|---|---|
|0x00|Not Ready to Switch On|
|0x40|Switch On Disabled|
|0x21|Ready to Switch On|
|0x23|Switched On|
|0x27|Operation Enabled|
|0x08 / 0x0F|Fault|

### 추가 감시 비트

- bit4: Voltage enabled (메인 전원 실제 인가)
- bit7: Warning
- bit10: Target reached (CSP/CSV)
- bit11: Internal limit active - 걸리면 명령값 무시될 수 있음
- bit12,13: 모드별 정의 상이

### 판단 원칙

- CW 전송 = 요청일 뿐, 즉시 전이 보장 안 됨
- 드라이브 내부 조건(버스전압, 인코더, 과전류 등) 통과해야 실제 전이
- 다음 사이클에 statusword 재확인 필수, 낙관적으로 다음 case로 넘어가면 안 됨
- 미전이 지속 시 타임아웃 처리 (통상 수백ms~1s)

---

## 슬레이브 종류별 판단 기준

|슬레이브 종류|Layer 1 (AL)|Layer 2 (응용 상태머신)|
|---|---|---|
|서보 드라이브 (CiA402)|거침, 필수|거침, CiA402 FSM 필요|
|FT센서 (RFT76-HA01, 벤더종속)|거침, 필수|**없음** - AL=OP+WKC 통과 즉시 데이터 신뢰|
|표준 I/O (CiA401)|거침, 필수|없음 - 디지털/아날로그 값 바로 사용|
|CiA404 준수 센서|거침, 필수|벤더가 상태비트 뒀으면 확인, 없으면 skip|

### 핵심 정리

- **정션박스/센서도 Layer 1(AL 상태머신)은 예외 없이 거침**
- Layer 2(CiA402 등 응용 상태머신)는 서보 드라이브류에만 존재하는 경우가 대부분
- "상태머신 안 거친다"는 표현은 부정확 → 정확히는 "**응용 계층** 상태머신이 없다"

---

## 코드 패턴 (IgH 기준)

```c
// 모든 슬레이브 공통 게이트
if (ds.wc_state != EC_WC_COMPLETE) goto safe_state;

// 여기서 슬레이브 타입별 분기
if (slave_type == SERVO_DRIVE) {
    sw = EC_READ_U16(domain_pd + off_statusword);
    switch (sw & 0x6F) {
        case 0x00:
        case 0x40: cw = 0x06; break;  // Shutdown
        case 0x21: cw = 0x07; break;  // Switch On
        case 0x23: cw = 0x0F; break;  // Enable Operation
        case 0x08:
        case 0x0F: cw = 0x80; break;  // Fault Reset
        default:   cw = 0x0F;
    }
    EC_WRITE_U16(domain_pd + off_controlword, cw);
} else if (slave_type == FT_SENSOR) {
    // 응용 상태머신 없음, WKC 통과 즉시 값 사용
    torque_x = EC_READ_S32(domain_pd + off_tx);
}
```