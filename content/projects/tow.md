---
title: "Tow"
slug: "tow"
description: "경량 에이전트리스 배포 오케스트레이터. Kubernetes 없이 베어메탈 서버와 클라우드 VM에 배포합니다."
date: 2026-03-26
icon: "fas fa-rocket"
iconGradient: "from-emerald-400 to-cyan-500"
version: "v0.2.0"
license: "MIT"
language: "Go"
github: "https://github.com/neurosamAI/tow-cli"
website: "https://tow-cli.neurosam.ai"
tags: ["Deployment", "DevOps", "CLI", "SSH", "Go", "Agentless", "MCP"]
install:
  - label: "Homebrew"
    command: "brew install neurosamAI/tap/tow"
  - label: "npm"
    command: "npm install -g @neurosamai/tow"
  - label: "Go"
    command: "go install github.com/neurosamAI/tow-cli/cmd/tow@latest"
  - label: "Binary"
    command: "curl -fsSL https://tow-cli.neurosam.ai/install.sh | sh"
features:
  - title: "에이전트리스 SSH 배포"
    icon: "fas fa-terminal"
    description: "대상 서버에 에이전트 설치가 필요 없습니다. SSH만 있으면 즉시 배포할 수 있습니다."
  - title: "심링크 기반 원자적 배포"
    icon: "fas fa-link"
    description: "심링크 전환으로 즉시 롤백이 가능합니다. 배포 중 다운타임을 최소화합니다."
  - title: "프로젝트 자동 감지"
    icon: "fas fa-magic"
    description: "tow init 한 줄로 프로젝트 타입, 프레임워크, 빌드 도구를 자동 감지하고 설정을 생성합니다."
  - title: "12개 내장 모듈 핸들러"
    icon: "fas fa-cubes"
    description: "Spring Boot, Node.js, Python, Go, Rust 등 12개 언어/프레임워크를 기본 지원합니다."
  - title: "35개 인프라 플러그인"
    icon: "fas fa-plug"
    description: "Kafka, Redis, MySQL, PostgreSQL, MongoDB, Elasticsearch 등 YAML 기반 플러그인을 제공합니다."
  - title: "4가지 헬스체크"
    icon: "fas fa-heartbeat"
    description: "HTTP, TCP, 로그 패턴, 커스텀 커맨드 — 네 가지 방식의 헬스체크를 기본 제공합니다."
  - title: "병렬 실행"
    icon: "fas fa-bolt"
    description: "여러 서버에 동시 배포합니다. 롤링 업데이트와 자동 롤백도 지원합니다."
  - title: "라이프사이클 훅"
    icon: "fas fa-code-branch"
    description: "빌드, 배포, 시작, 중지 전후로 커스텀 스크립트를 실행할 수 있습니다."
  - title: "AI 에이전트 연동"
    icon: "fas fa-robot"
    description: "MCP Server를 내장하여 Claude, Cursor, Windsurf 등 AI 에이전트와 네이티브로 연동됩니다."
comparison:
  headers: ["", "Tow", "Ansible", "Capistrano", "Kamal"]
  rows:
    - ["설치", "단일 바이너리", "Python 필요", "Ruby 필요", "Docker 필요"]
    - ["에이전트리스", "✓", "✓", "✓", "✗"]
    - ["Docker 불필요", "✓", "✓", "✓", "✗"]
    - ["프로젝트 자동 감지", "✓", "✗", "✗", "✗"]
    - ["내장 헬스체크", "4가지", "플러그인", "✗", "✓"]
    - ["즉시 롤백", "✓ (심링크)", "재실행 필요", "✓ (심링크)", "✓ (컨테이너)"]
    - ["다중 언어 네이티브", "12개 타입", "플레이북", "Ruby 중심", "Docker 이미지"]
    - ["멀티서버 로그 스트리밍", "✓ (색상 구분)", "✗", "✗", "✗"]
    - ["배포 전 diff 비교", "✓", "✗", "✗", "✗"]
    - ["AI 에이전트 연동 (MCP)", "✓", "✗", "✗", "✗"]
---

## Quick Start

Tow는 셸 스크립트와 Kubernetes 사이의 빈 공간을 채우는 배포 도구입니다. VM 기반 인프라에서 간편하고 안정적인 배포 파이프라인을 제공합니다.

### 기본 워크플로우

```bash
# 프로젝트 감지 & 설정 파일 생성
tow init

# 리모트 서버 초기화
tow setup -e prod -m api-server

# 원클릭 배포 (build → package → upload → deploy)
tow auto -e prod -m api-server

# 상태 확인
tow status -e prod -m api-server

# 즉시 롤백
tow rollback -e prod -m api-server
```

### 주요 커맨드

| 커맨드 | 설명 |
|--------|------|
| `tow init` | 프로젝트 자동 감지 & 설정 생성 |
| `tow auto` | 전체 파이프라인 실행 |
| `tow deploy` | 패키지 → 업로드 → 설치 → 재시작 |
| `tow status` | 모듈 상태 조회 (PID, 업타임, 메모리) |
| `tow rollback` | 이전 배포로 즉시 복원 |
| `tow logs` | 리모트 로그 스트리밍 (`--all`, `-F`, 프리셋) |
| `tow ssh` | 리모트 서버에 ad-hoc 명령 실행 |
| `tow diff` | 배포 전 로컬 vs 리모트 코드 비교 |
| `tow config` | CLI로 서버/모듈 설정 관리 |
| `tow provision` | 서버 프로비저닝 (타임존, JRE, 도구) |
| `tow mcp-server` | AI 에이전트용 MCP 서버 시작 |
