---
title: "video2text"
slug: "video2text"
description: "A fully local, speaker-diarized transcription app. It turns mp4 video/audio files into text organized by speaker, and no file ever leaves your machine."
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
  - title: "Fully Local Processing"
    icon: "fas fa-lock"
    description: "Both speech recognition and speaker diarization run entirely on Apple Silicon. Meeting content and voices are never sent to an external server."
  - title: "Automatic Voice Matching"
    icon: "fas fa-user-check"
    description: "Compares registered voice profiles against the diarization output using SpeechBrain speaker embeddings, and automatically matches names."
  - title: "Rematch / Relabel"
    icon: "fas fa-arrows-rotate"
    description: "If a speaker match is wrong or you add a profile later, you can rerun just the matching or manually fix the labels — without rerunning speech recognition and diarization from scratch."
  - title: "Self-Contained App Bundle"
    icon: "fas fa-box-archive"
    description: "Bundles the Python runtime, ffmpeg, and torch/mlx-whisper/pyannote dependencies all in one — just copy it to another Apple Silicon Mac and it works as-is."
  - title: "3 Export Formats"
    icon: "fas fa-file-export"
    description: "Download results as TXT (an easy-to-read transcript), SRT (video subtitles), or JSON (raw per-speaker blocks with timestamps)."
  - title: "Native Desktop UI"
    icon: "fas fa-desktop"
    description: "Convert files by drag-and-drop in a native macOS window built with pywebview, with progress shown in real time."
comparison:
  headers: ["", "video2text", "Otter.ai", "Whisper API", "Zoom AI Companion"]
  rows:
    - ["Processing location", "Fully local (on-device)", "Cloud", "Cloud", "Cloud"]
    - ["File upload", "Not required", "Required", "Required", "Required"]
    - ["Speaker diarization", "✓ (built-in)", "✓", "Requires manual implementation", "✓"]
    - ["Automatic voice matching", "✓", "✓ (account-based)", "✗", "✗"]
    - ["Rematch/relabel", "✓ (no pipeline rerun)", "✗", "✗", "✗"]
    - ["Cost", "Free (open source)", "Subscription", "Usage-based billing", "Subscription add-on"]
    - ["Offline use", "✓", "✗", "✗", "✗"]
    - ["Supported platforms", "macOS (Apple Silicon)", "Web/mobile", "API", "Web/app"]
---

## Quick Start

video2text is a fully local app: feed it an mp4 file (typically a video-conference recording) or an audio file, and it produces a speaker-diarized transcript. Whether it's an online meeting (split screen) or an in-person meeting recorded with a single camera and mixed audio, the same problem applies — multiple speakers are mixed into one audio track — so both cases go through the same pipeline (audio-based speaker diarization).

### Basic Workflow

No build required: grab `video2text-v1.0.0-macos-arm64.zip` from the [latest release](https://github.com/neurosamAI/video2text/releases/latest), unzip it, and double-click `video2text.app`.

To build it from source instead:

```bash
# Clone the repo & build the app bundle
git clone https://github.com/neurosamAI/video2text
cd video2text
./build.sh

# Run the desktop app (double-click video2text.app)
# Or run it as a web server from the terminal
./run.sh   # http://127.0.0.1:8765
```

### Usage Flow

1. **Register your voice profile** (optional, recommended) — enter your name and either record a short prompt or upload existing audio/video
2. **Convert an mp4** — drag in a file or select one, check which profiles to match, and start the conversion
3. **Check progress** — extract audio → diarize → transcribe → match speakers → done
4. **Download the results** — choose from TXT / SRT / JSON formats

### Components

| Component | Role |
|---|---|
| `pyannote/speaker-diarization-3.1` | Speaker diarization |
| `mlx-community/whisper-large-v3-turbo` | Speech recognition (Apple Silicon Metal acceleration) |
| `speechbrain/spkrec-ecapa-voxceleb` | Speaker embedding (automatic voice matching) |
| FastAPI + pywebview | Local web server + native macOS desktop shell |

The first run downloads each model's weights once from HuggingFace / Apple (mlx-community). After that, it runs completely offline.
