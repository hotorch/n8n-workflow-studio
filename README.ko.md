# n8n Workflow Studio 🚀

[English](README.md) | **한국어**

<p align="center">
  <img src="https://img.shields.io/badge/n8n-workflow-blue" alt="n8n">
  <img src="https://img.shields.io/badge/MCP-enabled-green" alt="MCP">
  <img src="https://img.shields.io/badge/AI-powered-purple" alt="AI">
  <img src="https://img.shields.io/badge/license-MIT-blue" alt="License">
</p>

# n8n MCP 워크플로우 개발 프로젝트

## 📌 프로젝트 개요

이 프로젝트는 **n8n-MCP (Model Context Protocol)** 도구를 활용하여 n8n 워크플로우를 효율적으로 개발하고 관리하기 위한 템플릿 저장소입니다. Claude Code와 MCP 도구를 통해 AI 지원 워크플로우 개발이 가능합니다.

## 🚀 빠른 시작 가이드

> **중요**: 이 섹션은 새로운 PC에서 프로젝트를 설정하는 완전한 가이드입니다.
> Claude Code 에이전트는 이 섹션을 참조하여 MCP 도구를 설치하고 설정할 수 있습니다.

### 1. MCP 도구 설정

이 프로젝트는 두 가지 필수 MCP 도구를 사용합니다:

#### n8n-mcp (필수)
- **용도**: n8n 워크플로우 생성 및 관리 도구
- **GitHub**: [https://github.com/czlonkowski/n8n-mcp](https://github.com/czlonkowski/n8n-mcp)
- **제공 기능**: 
  - 노드 검색 및 탐색
  - 워크플로우 검증
  - 템플릿 관리
  - AI 지원 워크플로우 생성
- **설치 명령**:
  ```bash
  # 방법 1: 로컬 서버 연결 (권장 - 가장 안정적)
  claude mcp add n8n-mcp -- npx -y @czlonkowski/n8n-mcp
  
  # 방법 2: 프로젝트 스코프로 추가 (프로젝트별 관리)
  claude mcp add n8n-mcp --scope project "npx @czlonkowski/n8n-mcp"
  ```

#### context7 (필수)
- **용도**: 라이브러리 문서 및 컨텍스트 관리 도구
- **GitHub**: [https://github.com/upstash/context7](https://github.com/upstash/context7)
- **제공 기능**:
  - 최신 라이브러리 문서 제공
  - 코드 예제 및 레퍼런스
  - 개발 컨텍스트 유지
- **설치 명령**:
  ```bash
  # 방법 1: 원격 서버 연결 (HTTP - 빠른 설정)
  claude mcp add --transport http context7 https://mcp.context7.com/mcp
  
  # 방법 2: SSE 전송 사용 (실시간 스트리밍)
  claude mcp add --transport sse context7 https://mcp.context7.com/sse
  
  # 방법 3: 로컬 서버 연결 (오프라인 작업 가능)
  claude mcp add context7 -- npx -y @upstash/context7-mcp
  ```

#### 자동 설정 vs 수동 설정

**자동 설정** (`.mcp.json` 파일이 있는 경우):
- 프로젝트에 이미 `.mcp.json` 파일이 포함되어 있음
- Claude Code 재시작 시 자동으로 MCP 도구 활성화
- 추가 설치 명령 불필요

**수동 설정** (새 환경 또는 `.mcp.json`이 없는 경우):
- 위의 설치 명령 실행 필요
- 각 도구별로 하나의 방법 선택
- 설치 후 Claude Code 재시작 필수

### 2. Claude Code 재시작
MCP 도구를 활성화하려면 Claude Code를 재시작해야 합니다:
1. Claude Code 종료
2. Claude Code 재실행
3. 프로젝트 폴더 열기
4. MCP 서버 사용 승인 (프롬프트 표시 시)

## 📁 프로젝트 구조

```
make-n8n-workflow/
├── .mcp.json                          # MCP 도구 설정 파일
├── .gitignore                         # Git 무시 규칙 (워크플로우 폴더 제외)
├── README.md                          # 영어 문서 (메인)
├── README.ko.md                       # 이 파일 (한글 가이드)
├── CLAUDE.md                          # Claude Code 개발 지침
├── make-workflow-instruction/         # n8n 개발 가이드 문서
│   ├── mcp-validation-patterns.md    # MCP 검증 패턴
│   ├── n8n-mcp-guide.md              # n8n-MCP 도구 사용 가이드
│   ├── n8n-workflow-creator.md       # 한글 워크플로우 생성 가이드
│   └── n8n-workflow-reference.md     # n8n 기능 레퍼런스
├── example-workflow-structure/        # 예제 폴더 구조 (Git에 포함)
│   └── README.md                      # 구조 설명서
└── [번호]-[워크플로우명]/             # 사용자 워크플로우 폴더 (로컬 전용 - Git 제외)
    ├── *.json                         # n8n 워크플로우 파일
    └── *.md                           # 워크플로우 설명 문서
```

> ⚠️ **주의**: 번호가 매겨진 워크플로우 폴더(`01-*/`, `02-*/` 등)는 자동으로 Git에서 제외되며 로컬 컴퓨터에만 저장됩니다.

### 워크플로우 폴더 관리 규칙

- **번호 체계**: `01-`, `02-`, `03-` ... 순차적 번호 부여
- **폴더명**: `[번호]-[설명적인-이름]` 형식
- **저장 위치**: 로컬 전용 (Git에 푸시되지 않음)
- **예시**: 
  - `01-reddit-workflow/` - Reddit 모니터링 워크플로우
  - `02-email-automation/` - 이메일 자동화 워크플로우
  - `03-data-pipeline/` - 데이터 파이프라인 워크플로우

> 💡 **보안 우선**: 사용자의 워크플로우는 로컬 컴퓨터에만 저장되며, 비즈니스 로직과 민감한 데이터를 보호합니다.

## 🛠 워크플로우 개발 가이드

### MCP 도구를 활용한 개발 프로세스

1. **문서 확인**
   - `make-workflow-instruction/` 폴더의 가이드 문서 참조
   - 특히 `n8n-mcp-guide.md`의 프로세스 따르기

2. **워크플로우 생성**
   ```
   Claude에게 요청 예시:
   "n8n-mcp 도구를 사용해서 이메일 자동화 워크플로우를 만들어주세요.
   make-workflow-instruction 폴더의 가이드를 참고해주세요."
   ```

3. **워크플로우 저장**
   - 새 워크플로우는 새 번호 폴더에 저장
   - 관련 문서와 함께 관리

### Claude Code 활용 팁

1. **MCP 도구 확인**
   ```
   /mcp list
   ```

2. **워크플로우 개발 시작**
   - n8n-mcp 도구 문서 먼저 확인: `tools_documentation()`
   - 노드 검색: `search_nodes()`
   - 워크플로우 검증: `validate_workflow()`

3. **가이드 문서 활용**
   - 항상 `make-workflow-instruction/` 폴더의 문서 참조
   - 한글 작업 시 `n8n-workflow-creator.md` 활용

## 📚 참고 문서

### 프로젝트 내 문서
- `make-workflow-instruction/n8n-mcp-guide.md` - MCP 도구 상세 가이드
- `make-workflow-instruction/n8n-workflow-creator.md` - 한글 워크플로우 생성 가이드
- `make-workflow-instruction/n8n-workflow-reference.md` - n8n 기능 전체 레퍼런스

### 외부 리소스
- [n8n-mcp GitHub](https://github.com/czlonkowski/n8n-mcp)
- [context7 GitHub](https://github.com/upstash/context7)
- [n8n 공식 문서](https://docs.n8n.io)
- [Claude Code MCP 문서](https://docs.anthropic.com/en/docs/claude-code/mcp)

## 🔄 워크플로우 예제

### 01-reddit-workflow
Reddit 커뮤니티 모니터링 및 텔레그램 알림 워크플로우
- 13개 AI/Tech 서브레딧 순회 모니터링
- 메타데이터 기반 점수 정규화
- AI 품질 필터링
- 텔레그램 자동 전송

## 🤝 협업 가이드

### 다른 PC에서 프로젝트 사용하기 (완전 가이드)

#### 단계 1: 저장소 클론
```bash
git clone [저장소 URL]
cd make-n8n-workflow
```

#### 단계 2: `.mcp.json` 파일 확인
```bash
# 파일 존재 여부 확인
ls -la .mcp.json
```

#### 단계 3: MCP 도구 설치

**경우 A: `.mcp.json` 파일이 있는 경우**
1. Claude Code 재시작
2. 프로젝트 폴더 열기
3. MCP 서버 승인 프롬프트에서 "승인" 선택
4. 자동으로 도구 활성화됨

**경우 B: `.mcp.json` 파일이 없거나 수동 설치가 필요한 경우**

```bash
# 필수 도구 1: n8n-mcp 설치
claude mcp add n8n-mcp -- npx -y @czlonkowski/n8n-mcp

# 필수 도구 2: context7 설치 (아래 중 하나 선택)
# 옵션 A: 원격 서버 (인터넷 연결 필요, 가장 빠름)
claude mcp add --transport http context7 https://mcp.context7.com/mcp

# 옵션 B: 로컬 서버 (오프라인 가능)
claude mcp add context7 -- npx -y @upstash/context7-mcp
```

#### 단계 4: Claude Code 재시작
1. Claude Code 완전히 종료 (모든 창 닫기)
2. Claude Code 다시 실행
3. 프로젝트 폴더 열기

#### 단계 5: MCP 도구 확인
```bash
# Claude Code 내에서 실행
/mcp list

# 다음과 같이 표시되어야 함:
# - n8n-mcp
# - context7
```

#### 단계 6: 설치 검증
Claude Code에서 다음 메시지 입력:
```
n8n-mcp 도구가 제대로 설치되었는지 확인해주세요.
tools_documentation() 명령을 실행해주세요.
```

#### 단계 7: 개발 시작
- CLAUDE.md 파일의 개발 지침 참조
- make-workflow-instruction/ 폴더의 가이드 문서 활용
- 새 워크플로우는 번호가 매겨진 폴더에 생성

## ⚠️ 주의사항

1. **MCP 도구 활성화**
   - 반드시 Claude Code 재시작 필요
   - 프로젝트 스코프 설정 확인

2. **워크플로우 검증**
   - 배포 전 항상 `validate_workflow()` 실행
   - 에러 처리 로직 포함

3. **폴더 구조 준수**
   - 새 워크플로우는 반드시 번호 폴더에 저장
   - 관련 문서 함께 관리

## 👥 기여하기

기여를 환영합니다! [Contributing Guidelines](CONTRIBUTING.md)를 참조해주세요.

## 📝 라이선스

MIT License - 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

## 🆘 문제 해결

### MCP 도구가 인식되지 않을 때

#### 진단 단계
1. **현재 상태 확인**
   ```bash
   # Claude Code 내에서
   /mcp list
   ```

2. **`.mcp.json` 파일 확인**
   ```bash
   cat .mcp.json
   ```

3. **수동 재설치**
   ```bash
   # 기존 설정 초기화
   claude mcp reset-project-choices
   
   # n8n-mcp 재설치
   claude mcp add n8n-mcp -- npx -y @czlonkowski/n8n-mcp
   
   # context7 재설치
   claude mcp add --transport http context7 https://mcp.context7.com/mcp
   ```

4. **Claude Code 완전 재시작**
   - 모든 Claude Code 창 닫기
   - 작업 관리자에서 Claude 프로세스 확인
   - Claude Code 다시 실행

5. **권한 문제 해결**
   ```bash
   # npx 캐시 정리
   npx clear-npx-cache
   
   # npm 캐시 정리
   npm cache clean --force
   ```

### 워크플로우 검증 오류
1. `validate_node_minimal()` 먼저 실행
2. 필수 필드 확인
3. 연결 구조 검증
4. 표현식 문법 확인

## 🔄 업데이트 내역

- 2025.01: 프로젝트 구조 개선 및 MCP 도구 통합
- 2025.01: Reddit 워크플로우 예제 추가
- 2025.01: 다국어 가이드 문서 추가

## 💬 지원 및 커뮤니티

- [GitHub Issues](https://github.com/yourusername/n8n-workflow-studio/issues) - 버그 리포트 및 기능 요청
- [Discussions](https://github.com/yourusername/n8n-workflow-studio/discussions) - 질문 및 아이디어 공유

## 🌟 프로젝트에 별 주기

이 프로젝트가 도움이 되었다면 ⭐를 눌러주세요!