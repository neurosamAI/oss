---
title: "video2text"
slug: "video2text"
description: "완전 로컬로 동작하는 화자 분리 전사 앱. mp4 영상/오디오 파일을 화자별로 정리된 텍스트로 바꿔주며, 어떤 파일도 외부로 전송되지 않습니다."
date: 2026-09-05
icon: "fas fa-closed-captioning"
iconGradient: "from-violet-400 to-fuchsia-500"
version: "v1.0.0"
license: "MIT"
language: "Python"
github: "https://github.com/neurosamAI/video2text"
website: "https://video2text.neurosam.ai"
tags: ["Transcription", "Speaker Diarization", "Whisper", "macOS", "Apple Silicon", "Privacy", "Local AI"]
install:
  - label: "Download (macOS, Apple Silicon)"
    command: "curl -LO https://github.com/neurosamAI/video2text/releases/latest/download/video2text-v1.0.0-macos-arm64.zip"
  - label: "Build from source"
    command: "git clone https://github.com/neurosamAI/video2text && cd video2text && ./build.sh"
features:
  - title: "완전 로컬 처리"
    icon: "fas fa-lock"
    description: "음성 인식과 화자 분리 모두 Apple Silicon 안에서만 실행됩니다. 회의 내용과 목소리가 외부 서버로 전송되지 않습니다."
  - title: "내 목소리 자동 매칭"
    icon: "fas fa-user-check"
    description: "SpeechBrain 화자 임베딩으로 등록된 목소리 프로필과 화자 분리 결과를 비교해 이름을 자동으로 매칭합니다."
  - title: "재매칭 / 재라벨링"
    icon: "fas fa-arrows-rotate"
    description: "화자 매칭이 틀렸거나 프로필을 나중에 추가해도, 음성 인식·화자 분리를 처음부터 재실행하지 않고 매칭만 다시 돌리거나 라벨을 직접 고칠 수 있습니다."
  - title: "독립 실행형 앱 번들"
    icon: "fas fa-box-archive"
    description: "Python 런타임과 ffmpeg, torch/mlx-whisper/pyannote 의존성을 통째로 담은 번들이라 다른 Apple Silicon Mac에 복사만 해도 그대로 동작합니다."
  - title: "3가지 내보내기 포맷"
    icon: "fas fa-file-export"
    description: "TXT(읽기 편한 전사본), SRT(영상 자막), JSON(화자별 블록 + 타임스탬프 원본)으로 결과를 내려받습니다."
  - title: "네이티브 데스크톱 UI"
    icon: "fas fa-desktop"
    description: "pywebview 기반 네이티브 macOS 창에서 드래그 앤 드롭으로 변환하고, 진행 상황을 실시간으로 확인합니다."
comparison:
  headers: ["", "video2text", "Otter.ai", "Whisper API", "Zoom AI Companion"]
  rows:
    - ["처리 위치", "완전 로컬(온디바이스)", "클라우드", "클라우드", "클라우드"]
    - ["파일 업로드", "불필요", "필요", "필요", "필요"]
    - ["화자 분리", "✓ (내장)", "✓", "직접 구현 필요", "✓"]
    - ["내 목소리 자동 매칭", "✓", "✓ (계정 기반)", "✗", "✗"]
    - ["재매칭/재라벨링", "✓ (파이프라인 재실행 없음)", "✗", "✗", "✗"]
    - ["비용", "무료 (오픈소스)", "구독", "사용량 과금", "구독 부가"]
    - ["오프라인 사용", "✓", "✗", "✗", "✗"]
    - ["지원 플랫폼", "macOS(Apple Silicon)", "웹/모바일", "API", "웹/앱"]
---

## Quick Start

video2text는 mp4(주로 화상회의 녹화본)나 오디오 파일을 넣으면 화자 분리(diarization)된 텍스트 전사본을 만들어주는 완전 로컬 앱입니다. 온라인 회의(화면 분할)든 오프라인 회의 녹화(단일 카메라 + 믹스된 오디오)든, 오디오 트랙 하나에 여러 화자가 섞여 들어온다는 점은 동일하므로 같은 파이프라인(오디오 기반 화자 분리)으로 처리합니다.

### 기본 워크플로우

빌드 없이 바로 쓰려면 [최신 릴리즈](https://github.com/neurosamAI/video2text/releases/latest)에서
`video2text-v1.0.0-macos-arm64.zip`을 받아 압축을 풀고 `video2text.app`을 더블클릭하면 됩니다.

직접 빌드하려면:

```bash
# 저장소 클론 & 앱 번들 빌드
git clone https://github.com/neurosamAI/video2text
cd video2text
./build.sh

# 데스크톱 앱 실행 (video2text.app 더블클릭)
# 또는 터미널에서 웹 서버로 실행
./run.sh   # http://127.0.0.1:8765
```

### 사용 흐름

1. **내 목소리 프로필 등록** (선택, 추천) — 이름을 입력하고 짧은 문장을 녹음하거나 기존 오디오/영상을 업로드
2. **mp4 변환** — 파일을 드래그하거나 선택하고 매칭할 프로필을 체크한 뒤 변환 시작
3. **진행 상황 확인** — 오디오 추출 → 화자 분리 → 음성 인식 → 화자 매칭 → 완료
4. **결과 다운로드** — TXT / SRT / JSON 중 원하는 형식 선택

### 구성 요소

| 컴포넌트 | 역할 |
|---|---|
| `pyannote/speaker-diarization-3.1` | 화자 분리 |
| `mlx-community/whisper-large-v3-turbo` | 음성 인식 (Apple Silicon Metal 가속) |
| `speechbrain/spkrec-ecapa-voxceleb` | 화자 임베딩 (내 목소리 자동 매칭) |
| FastAPI + pywebview | 로컬 웹 서버 + 네이티브 macOS 데스크톱 셸 |

처음 실행 시 각 모델 가중치를 HuggingFace / Apple(mlx-community)에서 한 번 내려받습니다. 이후에는 완전히 오프라인으로 동작합니다.
