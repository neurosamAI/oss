---
title: "Tow"
slug: "tow"
description: "A lightweight, agentless deployment orchestrator. Deploy to bare-metal servers and cloud VMs without Kubernetes."
date: 2026-03-26
icon: "fas fa-rocket"
iconGradient: "from-emerald-400 to-cyan-500"
version: "v0.3.1"
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
  - title: "Agentless SSH Deployment"
    icon: "fas fa-terminal"
    description: "No agent needs to be installed on target servers. All you need is SSH to deploy instantly."
  - title: "Symlink-Based Atomic Deployment"
    icon: "fas fa-link"
    description: "A symlink switch enables instant rollback. Minimizes downtime during deployment."
  - title: "Project Auto-Detection"
    icon: "fas fa-magic"
    description: "A single `tow init` command auto-detects your project type, framework, and build tool, then generates the configuration."
  - title: "12 Built-in Module Handlers"
    icon: "fas fa-cubes"
    description: "Supports 12 languages/frameworks out of the box, including Spring Boot, Node.js, Python, Go, and Rust."
  - title: "35+ Infrastructure Plugins"
    icon: "fas fa-plug"
    description: "Built-in plugins for Kafka, Redis, MySQL, PostgreSQL, and more, plus a community plugin ecosystem (tow plugin add)."
  - title: "4 Health Check Types"
    icon: "fas fa-heartbeat"
    description: "HTTP, TCP, log pattern, and custom command — four built-in health check methods."
  - title: "Parallel Execution"
    icon: "fas fa-bolt"
    description: "Deploy to multiple servers simultaneously. Also supports rolling updates and automatic rollback."
  - title: "Lifecycle Hooks"
    icon: "fas fa-code-branch"
    description: "Run custom scripts before and after build, deploy, start, and stop."
  - title: "AI Agent Integration"
    icon: "fas fa-robot"
    description: "A built-in MCP server enables native integration with AI agents like Claude, Cursor, and Windsurf."
  - title: "Deployment Metrics"
    icon: "fas fa-chart-bar"
    description: "Use tow metrics to view deployment frequency, action breakdowns, and per-module statistics as bar charts."
  - title: "Interactive Selection"
    icon: "fas fa-hand-pointer"
    description: "Omit the server/module flags for an interactive prompt. View logs from multiple modules at once using comma-separated names."
comparison:
  headers: ["", "Tow", "Ansible", "Capistrano", "Kamal"]
  rows:
    - ["Install", "Single binary", "Requires Python", "Requires Ruby", "Requires Docker"]
    - ["Agentless", "✓", "✓", "✓", "✗"]
    - ["No Docker needed", "✓", "✓", "✓", "✗"]
    - ["Project auto-detection", "✓", "✗", "✗", "✗"]
    - ["Built-in health checks", "4 types", "Plugin", "✗", "✓"]
    - ["Instant rollback", "✓ (symlink)", "Re-run needed", "✓ (symlink)", "✓ (container)"]
    - ["Multi-language support", "12 types", "Playbooks", "Ruby-centric", "Docker images"]
    - ["Multi-server log streaming", "✓ (color-coded)", "✗", "✗", "✗"]
    - ["Pre-deploy diff comparison", "✓", "✗", "✗", "✗"]
    - ["AI agent integration (MCP)", "✓", "✗", "✗", "✗"]
    - ["Deployment metrics", "✓", "✗", "✗", "✗"]
    - ["Interactive selection", "✓", "✗", "✗", "✗"]
    - ["Community plugins", "✓", "Galaxy", "✗", "✗"]
---

## Quick Start

Tow is a deployment tool that fills the gap between shell scripts and Kubernetes. It provides a simple, reliable deployment pipeline for VM-based infrastructure.

### Basic Workflow

```bash
# Detect project & generate config file
tow init

# Initialize remote server
tow setup -e prod -m api-server

# One-click deploy (build → package → upload → deploy)
tow auto -e prod -m api-server

# Check status
tow status -e prod -m api-server

# Instant rollback
tow rollback -e prod -m api-server
```

### Main Commands

| Command | Description |
|--------|------|
| `tow init` | Auto-detect project & generate config |
| `tow auto` | Run the full pipeline |
| `tow deploy` | Package → upload → install → restart |
| `tow status` | Check module status (PID, uptime, memory) |
| `tow rollback` | Instantly restore the previous deployment |
| `tow logs` | Stream remote logs (`--all`, `-F`, presets) |
| `tow ssh` | Run ad-hoc commands on remote servers |
| `tow diff` | Compare local vs remote code before deploying |
| `tow config` | Manage server/module configuration via CLI |
| `tow metrics` | View deployment frequency and per-action/module statistics |
| `tow plugin` | Install/remove community plugins |
| `tow provision` | Provision a server (timezone, JRE, tools) |
| `tow mcp-server` | Start the MCP server for AI agent integration |
