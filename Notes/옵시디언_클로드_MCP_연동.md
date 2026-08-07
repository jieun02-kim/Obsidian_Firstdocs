# 옵시디언 ↔ Claude Desktop MCP 연동 가이드

## 준비물
- Claude Desktop 앱 (Mac/Windows)
- Node.js 설치
- 옵시디언 커뮤니티 플러그인: **Local REST API**

## 순서

### 1. 옵시디언 설정
- 설정 → Community plugins → "Local REST API" 검색 후 설치·활성화
- 플러그인이 생성해주는 **API 키** 복사해두기

### 2. Claude Desktop 설정 파일 열기
- Mac: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

### 3. 설정 파일에 MCP 서버 추가
```json
{
  "mcpServers": {
    "obsidian": {
      "command": "npx",
      "args": ["-y", "obsidian-mcp-server-패키지명"],
      "env": {
        "OBSIDIAN_API_KEY": "여기에_복사한_API_키"
      }
    }
  }
}
```
> 실제 패키지명은 최신 버전 확인 필요 (npm에 "obsidian mcp"로 검색)

### 4. Claude Desktop 재시작
- 대화창 하단 도구(🔌) 아이콘에서 옵시디언 연결 확인

## 핵심 포인트
- 지금 쓰는 웹/모바일 채팅 ❌ → 로컬 접근 불가
- Claude Desktop 앱 ✅ → 내 컴퓨터에서 실행되므로 로컬 MCP 서버 연결 가능
- Local REST API 플러그인이 옵시디언과 MCP 서버 사이의 다리 역할
