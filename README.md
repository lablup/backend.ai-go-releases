# Backend.AI GO

**An agentic workflow platform with cross-platform local AI serving: private, fast, and under your control.**

Backend.AI GO is a desktop application and headless server for running AI models, building agentic workflows, and connecting local, remote, and cloud inference in one interface. It can run text and vision-language models, generate images, transcribe audio, ground conversations in a local document library, coordinate multi-agent squads, and expose OpenAI-compatible and management APIs.

This public repository distributes Backend.AI GO installers, command-line and headless-server packages, checksums, SBOMs, and updater metadata.

## Key Features

### Local and Containerized Inference

- Search, download, and manage GGUF and MLX models from Hugging Face.
- Run hardware-specific engines for Apple Metal, NVIDIA CUDA, AMD ROCm/HIP, Intel SYCL/Vulkan, or CPU-only systems.
- Install and update engine and runtime packages from the in-app **Engines** page.
- Run managed vLLM and SGLang container engines for high-throughput safetensors serving on supported NVIDIA hosts.
- Use speculative decoding, including draft-model and embedded-MTP paths when the selected model and engine support them.

Local inference requests stay on the machine or nodes you select. Cloud providers, web search, external connectors, and remote MCP servers send data to their configured services when you enable and use them.

### Local, Remote, and Cloud Models

Backend.AI GO provides one model picker and routing layer for:

- OpenAI, including API-key access and ChatGPT Codex OAuth
- Anthropic
- Google Gemini
- Azure OpenAI
- OpenAI-compatible endpoints
- Remote vLLM, Ollama, LM Studio, llama.cpp, mlxcel, and Continuum Router endpoints

Provider catalogs and capabilities are probed through the router. If more than one provider serves the same model ID, Backend.AI GO keeps each provider selectable and routes the request to the chosen backend.

### Agents, Cowork, and Squads

- **Agent execution**: Multi-step tool use with web, file, code, data, image, and app-control tools.
- **Cowork execution mode**: Persistent multi-turn workspaces, sub-agent delegation, inline `@agent` dispatch, live steps, and approval handling.
- **Agent Squad**: Specialized agents working through a shared workspace, planner, task board, execution reports, and activity dashboard.
- **Discussion Rooms**: Moderated, brainstorm, round-robin, and autonomous multi-agent discussions with turn budgets and conclusion synthesis.
- **Governance**: Tool approvals, guardrails, spending and rate limits, policy evaluation, notifications, and durable audit records.
- **ACP and Extensions**: Agent Communication Protocol profiles plus imports for `SKILL.md` skills, Claude Code sub-agents, and Codex `AGENTS.md` definitions.

### Data, Memory, and Creative Workflows

- **Data Hub**: Ingest files, folders, and URLs into a local library; search with lexical or hybrid retrieval; and ground chat responses with citations.
- **Data Wiki**: Generate and maintain a wiki from library content with scheduled sweeps and diagnostic checks.
- **Memory**: Namespace-based conversation memory with extraction, deduplication, browsing, and maintenance tools.
- **Draw and Creations**: Generate images locally through stable-diffusion.cpp or through configured cloud providers, then manage outputs in a gallery.
- **Audio transcription**: Transcribe speech locally through whisper.cpp.
- **Document translation**: Translate text, OCR-extracted images, TXT, Markdown, DOCX, and PDF content with glossary support.
- **Automations**: Schedule recurring tasks with cron expressions, templates, input sources, tool permissions, and output actions.

### Extensibility and Connectivity

- **MCP**: Connect stdio, Streamable HTTP, and legacy HTTP+SSE MCP servers; expose Backend.AI GO's own MCP endpoint; and render MCP Apps tool results.
- **Plugins**: Extend the application through a plugin SDK, UI slots, scoped storage, and agent-tool permissions.
- **External connectors**: Use Email (SMTP/IMAP) and Google Calendar with OS-backed credential storage, audit logs, and undo support.
- **Claude Code integration**: Route Anthropic-compatible requests through model aliases and optionally augment web search through Serper, Brave, or Exa.

### APIs, Headless Operation, and Multi-Node Serving

- Serve OpenAI-compatible chat, completion, model, and image endpoints.
- Use the Management REST API, server-sent events, and the `aigo` CLI from desktop or headless deployments.
- Connect Backend.AI GO instances and Backend.AI clusters through mDNS discovery, QR registration, or `aigo://` deep links.
- Route registered-node models into chat and use distributed pipeline serving on compatible node groups.
- Apply managed endpoints, signed policy, feature gates, internal mirrors, and air-gapped deployment profiles in enterprise environments.

## System Requirements

Resource needs depend primarily on the model and context size. A model must fit in available RAM, unified memory, or VRAM together with its runtime and KV cache.

| Component      | Minimum    | Recommended                       |
| -------------- | ---------- | --------------------------------- |
| RAM            | 8 GB       | 16 GB or more                     |
| Storage        | 10 GB free | 50 GB or more for multiple models |
| GPU (optional) | 4 GB VRAM  | 8 GB or more VRAM                 |

### Platform Support

| Platform | Architecture          | Requirements and packages                                                                                                                                                                                                    |
| -------- | --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| macOS    | Apple Silicon (arm64) | macOS 15 Sequoia or later; Intel Macs are not supported. DMG desktop installer plus CLI and headless-server archives.                                                                                                        |
| Windows  | x64                   | Windows 10 or 11. Signed NSIS desktop installer and standalone CLI; no Windows headless-server package.                                                                                                                      |
| Linux    | x64, arm64            | Desktop `.deb`, AppImage, and Flatpak bundles plus CLI and headless-server packages. The one-line CLI/server installer requires glibc 2.39 or later (Ubuntu 24.04+); use the container image on older glibc or musl systems. |

## Installation

Download the [latest stable release](https://github.com/lablup/backend.ai-go-releases/releases/latest), or browse [all releases and prereleases](https://github.com/lablup/backend.ai-go-releases/releases).

Each release publishes `SHA256SUMS.txt` for integrity verification and a compressed CycloneDX SBOM. The main desktop assets are:

| Platform        | Release asset                                                                          |
| --------------- | -------------------------------------------------------------------------------------- |
| macOS desktop   | `backend-ai-go-<version>-macos-arm64.dmg`                                              |
| Windows desktop | `backend-ai-go-<version>-windows-x64-setup.exe`                                        |
| Linux desktop   | `backend-ai-go-<version>-linux-{x64,arm64}.deb`                                        |
| Linux portable  | `backend-ai-go-<version>-linux-{x64,arm64}.AppImage`                                   |
| Linux Flatpak   | `backend-ai-go-<version>-linux-{x64,arm64}.flatpak`                                    |
| CLI             | `aigo-cli-{macos,linux,windows}-<architecture>.*`                                      |
| Headless server | `aigo-server-<version>-linux-{x64,arm64}.deb` or platform archives for macOS and Linux |

### One-Line Install for the CLI and Headless Server

On macOS or Linux:

```bash
curl -fsSL https://go.backend.ai/install.sh | sh
```

On Windows PowerShell:

```powershell
irm https://go.backend.ai/install.ps1 | iex
```

The macOS/Linux installer installs `aigo` and `aigo-server` into `~/.aigo/bin` and adds that directory to `PATH`. The Windows installer installs `aigo` only. Every downloaded archive is checked against the release's `SHA256SUMS.txt`, and the verification cannot be skipped.

Common macOS/Linux options:

```bash
# CLI only, without a confirmation prompt
curl -fsSL https://go.backend.ai/install.sh | sh -s -- --cli-only -y

# Latest prerelease
curl -fsSL https://go.backend.ai/install.sh | sh -s -- --channel beta

# System-wide Linux install with a systemd service
curl -fsSL https://go.backend.ai/install.sh | sudo sh -s -- --system
```

The installer also supports exact-version pins, custom prefixes, dry runs, mirrors, and uninstall. See the [installation guide](https://go.backend.ai/en/manual/getting-started/installation/) for the complete option and platform matrix.

### Homebrew

The Lablup tap provides the macOS desktop app and the CLI/server formulas for macOS and Linux:

```bash
brew tap lablup/tap

# Desktop app (macOS 15+ on Apple Silicon)
brew install --cask backend-ai-go

# CLI client
brew install aigo-cli

# Headless server
brew install aigo-server
```

### Manual Desktop Installation

#### macOS

1. Download the arm64 `.dmg`.
2. Open it and drag **Backend.AI GO** to **Applications**.
3. Launch the application and complete the first-time setup wizard.

#### Windows

1. Download and run the x64 `-setup.exe` installer.
2. Follow the installation wizard.
3. Keep GPU drivers current if you use hardware acceleration.

#### Linux

Replace `<version>` and `x64` with the release and architecture you downloaded.

```bash
# Debian/Ubuntu package (installs dependencies through apt)
sudo apt install ./backend-ai-go-<version>-linux-x64.deb

# AppImage (portable)
chmod +x backend-ai-go-<version>-linux-x64.AppImage
./backend-ai-go-<version>-linux-x64.AppImage

# Flatpak bundle
flatpak install --user ./backend-ai-go-<version>-linux-x64.flatpak
flatpak run ai.backend.go
```

## Quick Start

### 1. Complete First-Time Setup

On first launch, choose the interface language, review the detected accelerator, select a models directory, and optionally configure a first local model and cloud providers. All of these choices can be changed later.

### 2. Download a Model

- Open **Models > Browse**.
- Choose a model that fits your available memory.
- Use GGUF for the broadest engine and platform compatibility, or MLX on a supported mlxcel/MLX setup.
- For GGUF models, `Q4_K_M` is usually a practical starting point for the size/quality tradeoff.

### 3. Load the Model

- Open **Models > Local**.
- Select the downloaded model and click **Load**.
- If prompted, install the engine variant recommended for the detected hardware.
- Wait until the model reports that it is ready.

### 4. Start a Conversation

Open **Home** or **Chat**, choose the loaded model, and send a message. After the model and engine are installed, ordinary local inference does not require an internet connection unless the workflow uses an online tool, provider, connector, or remote node.

## Supported Inference Engines

Engine packages are installed separately from the application, so the exact variants offered depend on the platform and detected hardware.

| Engine                                                                 | Model format             | Platform                                           | Role                                                                                                  |
| ---------------------------------------------------------------------- | ------------------------ | -------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| [llama.cpp](https://github.com/ggml-org/llama.cpp)                     | GGUF                     | Supported desktop platforms                        | General text and vision-language inference with CPU, Metal, CUDA, ROCm/HIP, SYCL, and Vulkan variants |
| [MLX LM](https://github.com/ml-explore/mlx-lm)                         | MLX, GGUF                | macOS arm64                                        | Legacy Apple MLX compatibility path                                                                   |
| [mlxcel](https://github.com/lablup/mlxcel)                             | MLX                      | macOS arm64 (Metal), Linux x64/arm64 (NVIDIA CUDA) | Preferred native MLX serving engine for LLMs and VLMs                                                 |
| [vLLM](https://github.com/vllm-project/vllm)                           | Safetensors repositories | Managed containers on supported NVIDIA hosts       | High-throughput serving                                                                               |
| [SGLang](https://github.com/sgl-project/sglang)                        | Safetensors repositories | Managed containers on supported NVIDIA hosts       | Prefix caching and structured-output serving                                                          |
| [stable-diffusion.cpp](https://github.com/leejet/stable-diffusion.cpp) | Safetensors, CKPT, GGUF  | Supported desktop platforms                        | Local image generation                                                                                |
| [whisper.cpp](https://github.com/ggml-org/whisper.cpp)                 | GGUF, BIN                | Supported desktop platforms                        | Local speech-to-text transcription                                                                    |

`mlxcel` provides a native Rust CLI and an OpenAI-compatible server for MLX text and vision-language models. Its serving stack includes continuous batching, automatic prefix caching, speculative and MTP decoding, KV-cache controls, model surgery, and multi-device or distributed execution for supported configurations. It is optimized for Apple Silicon, also supports NVIDIA CUDA on Linux, and includes an experimental OpenXLA backend under active development.

## Updates

Backend.AI GO supports stable, beta, and canary update channels. By default it checks on startup and can download an available standalone-app update in the background, then shows an update-ready badge before restart and installation. Package-managed installations are given the appropriate upgrade command instead of being overwritten by the in-app updater. You can change update behavior or run a manual check from Settings or the Help menu.

## Documentation

- [English manual](https://go.backend.ai/en/manual/)
- [Korean manual](https://go.backend.ai/ko/manual/)
- [Official website](https://go.backend.ai/)

## Support

- Report bugs and request features in [GitHub Issues](https://github.com/lablup/backend.ai-go-releases/issues).
- Ask questions and meet the community on [Backend.AI Discord](https://discord.gg/backend-ai).

## License

Backend.AI GO release builds are distributed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0). They may be downloaded, used, modified, and redistributed in accordance with the license. This repository provides prebuilt packages; the Backend.AI GO source code is not published.

The source code for [mlxcel](https://github.com/lablup/mlxcel) is publicly available under the Apache License 2.0. Third-party components remain subject to their respective license terms and notices.

Backend.AI GO is developed and maintained by [Lablup Inc.](https://www.lablup.com) as part of the [Backend.AI project](https://www.backend.ai/).
