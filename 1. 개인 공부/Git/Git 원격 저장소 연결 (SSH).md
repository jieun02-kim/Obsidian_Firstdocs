# Git 원격 저장소 처음 연결하기

상황: 원격 저장소는 이미 GitHub에 있고, 내 PC에 처음 가져오는 경우

## 1. Git 설치 확인
```bash
git --version
```

## 2. SSH 키 준비 (계정당 1회만)
이미 있으면 생략:
```bash
ls -la ~/.ssh/id_ed25519.pub   # 있는지 확인
```
없으면 생성:
```bash
ssh-keygen -t ed25519 -C "본인이메일@example.com"
```

## 3. GitHub에 공개키 등록 (계정당 1회만)
```bash
cat ~/.ssh/id_ed25519.pub   # 이 내용 복사
```
GitHub → Settings → SSH and GPG keys → New SSH key → 붙여넣기

등록 확인:
```bash
ssh -T git@github.com
# "Hi <계정명>! You've successfully authenticated..." 뜨면 성공
```

## 4. 원격 저장소를 처음 로컬로 가져오기
`git init` 필요 없음 — clone이 init까지 알아서 해줌. 처음부터 SSH 주소로 clone:
```bash
git clone git@github.com:계정명/저장소이름.git
```
→ 이 한 줄로 로컬 저장소 생성 + origin 자동 등록(SSH) + main 브랜치 추적까지 전부 끝.

## 5. 이후 작업
```bash
cd 저장소이름
# 파일 수정...
git add .
git commit -m "메시지"
git push          # SSH라서 비밀번호/토큰 없이 바로 push
```

---

## 참고: git init이 필요한 경우
로컬에 이미 파일이 있고, 거기에 새 원격 저장소를 연결하고 싶을 때만 사용:
```bash
git init
git remote add origin git@github.com:계정/새저장소.git
git add .
git commit -m "first commit"
git push -u origin main
```

---

## 핵심 요약
- SSH 키 생성 + GitHub 등록(1~3번): **이 PC에서 평생 1회만**
- 새 저장소마다: **SSH 주소로 clone(4번)만 반복**하면 인증 문제 없이 바로 push 가능
- 실수로 HTTPS 주소로 clone했다면:
  ```bash
  git remote set-url origin git@github.com:계정/저장소.git
  ```
