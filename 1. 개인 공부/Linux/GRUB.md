# GRUB (GRand Unified Bootloader)

리눅스에서 가장 널리 쓰이는 부트로더. 전원이 켜진 뒤 커널을 메모리에 올리기 전, 어떤 OS/커널로 부팅할지 선택하고 넘겨주는 역할을 함.

## 부팅 방식과 파티션 (BIOS/MBR vs UEFI/GPT)

펌웨어가 디스크의 어디서 부트로더를 찾는지가 두 방식으로 나뉘고, 이에 따라 디스크 파티션 방식도 짝을 이룸.

| | 레거시 BIOS | UEFI |
|---|---|---|
| 파티션 방식 | MBR (Master Boot Record) | GPT (GUID Partition Table) |
| 부트로더 위치 | 디스크 맨 앞 512바이트(MBR)에 직접 설치 | 별도 파티션(**ESP**)의 파일 형태로 설치 |
| 파티션 개수 제한 | 기본 4개(주 파티션) | 사실상 제한 없음 |
| 디스크 용량 한계 | 2TB | 없음(사실상) |

### EFI System Partition (ESP)
- UEFI 방식에서 부트로더·커널 로더가 실제로 저장되는 FAT32 포맷의 별도 파티션. 보통 100MB~500MB 크기로, `/boot/efi`에 마운트됨
- 내부에 `EFI/<배포판이름>/grubx64.efi`, `EFI/Microsoft/Boot/bootmgfw.efi`처럼 OS/배포판별 폴더가 나뉘어 있어 **하나의 ESP를 여러 OS가 공유**할 수 있음 — Windows·리눅스 듀얼 부팅 시 ESP를 새로 만들지 않고 기존 것을 그대로 쓰는 이유
- 확인 명령:
```bash
lsblk -f              # 파티션 목록에서 타입이 vfat이고 /boot/efi에 마운트된 것이 ESP
efibootmgr -v         # UEFI가 인식하고 있는 부팅 항목 목록 확인
```

### GRUB 설치 시 방식별 차이
```bash
# UEFI 시스템 — ESP(/boot/efi)에 grub 파일을 설치
sudo grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB

# 레거시 BIOS 시스템 — 디스크 자체(MBR)에 설치, 파티션이 아니라 디스크를 지정
sudo grub-install --target=i386-pc /dev/sda
```
- 지금 시스템이 어느 방식인지는 `[ -d /sys/firmware/efi ] && echo UEFI || echo BIOS`로 확인 가능

## 주요 설정 파일
- `/etc/default/grub` — 사용자가 직접 편집하는 설정 (타임아웃, 기본 부팅 항목, 커널 파라미터 등). 여기 수정 후 반드시 아래 update 명령을 실행해야 반영됨
- `/boot/grub/grub.cfg` (또는 `/boot/grub2/grub.cfg`) — 실제 부팅 시 읽는 최종 설정 파일. 자동 생성되므로 직접 수정하지 않음
- `/etc/grub.d/` — grub.cfg를 생성할 때 조합되는 스크립트 조각들 (예: `40_custom`에 사용자 정의 부팅 항목 추가)

## 자주 쓰는 명령어
```bash
sudo update-grub                     # Debian/Ubuntu 계열: grub.cfg 재생성
sudo grub2-mkconfig -o /boot/grub2/grub.cfg   # RHEL/Fedora 계열: 위와 동일한 역할
sudo grub-install /dev/sda           # 부트로더 자체를 디스크(MBR/GPT)에 (재)설치
```

## /etc/default/grub 주요 옵션
```bash
GRUB_DEFAULT=0            # 기본으로 부팅할 항목 번호 (0=목록 첫 번째)
GRUB_TIMEOUT=5            # 메뉴 표시 후 자동 부팅까지 대기 시간(초)
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"   # 커널에 전달할 부팅 파라미터
GRUB_DISABLE_OS_PROBER=false   # 다른 OS(Windows 등) 자동 탐지 여부
```

## 듀얼 부팅에서 다른 OS가 메뉴에 안 뜰 때
1. `GRUB_DISABLE_OS_PROBER=false`로 설정돼 있는지 확인 (`/etc/default/grub`)
2. `sudo os-prober` 실행해서 다른 OS가 탐지되는지 확인
3. `sudo update-grub`로 grub.cfg 재생성

## 부팅이 안 될 때 (GRUB rescue / grub> 프롬프트)
- 파티션이 깨졌거나 grub.cfg를 못 찾을 때 진입. `ls`로 파티션 목록 확인 후 커널 위치를 수동으로 지정해 임시 부팅 가능:
```
grub rescue> ls
grub rescue> set root=(hd0,gpt2)
grub rescue> set prefix=(hd0,gpt2)/boot/grub
grub rescue> insmod normal
grub rescue> normal
```
- 임시 부팅에 성공하면, 정상 부팅한 뒤 `grub-install` + `update-grub`로 근본 원인(부트로더 재설치) 해결

## 참고
- Windows와 듀얼 부팅 시, Windows 업데이트가 부트로더를 자체 것으로 덮어써서 GRUB이 사라지는 경우가 흔함 → 위 rescue 절차 또는 Live USB로 부팅해 `grub-install` 재실행으로 복구
