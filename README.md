# Backend.AI GO

**An agentic workflow platform with cross-platform local LLM serving: private, fast, and fully under your control.**

Backend.AI GO is a cross-platform desktop application for building and running agentic AI workflows on your own machine. Run Large Language Models (LLMs), generate images, transcribe audio, and orchestrate multi-agent squads locally. Download models from Hugging Face, chat with AI privately, connect to cloud providers, or scale to other Backend.AI GO instances and enterprise clusters when you need more power.

## Key Features

### Local AI Inference
Run popular models like Gemma 3, Qwen3, Llama, and Mistral entirely on your hardware. Your conversations stay on your machine, so no data leaves your computer.

### Hardware Acceleration
- **Apple Silicon (MLX)**: Native acceleration for M1/M2/M3/M4/M5 chips
- **NVIDIA GPU (CUDA)**: Full GPU acceleration on Windows and Linux
- **AMD GPU (HIP/ROCm)**: Support for AMD graphics cards
- **Intel GPU (SYCL)**: Acceleration for Intel Arc and Iris graphics
- **CPU**: Optimized inference for systems without dedicated GPUs

### Hybrid Cloud Integration
Seamlessly combine local models with cloud APIs. Use local models for sensitive data, switch to GPT, Claude, or Gemini for complex tasks, all from the same interface. Provider capability detection probes each model so the app only sends features (tool calls, context length) the model actually supports.

Supported providers:
- OpenAI (GPT-5.2, GPT Image 1.5, via API key or ChatGPT sign-in)
- Anthropic (Claude Opus 4.8, Claude Sonnet 4.6)
- Google (Gemini 3 Pro, Gemini 3 Flash)
- Any OpenAI-compatible endpoint (Ollama, LocalAI, vLLM, etc.)

### AI Agents and Multi-Agent Squads
Turn your AI from a simple chatbot into an autonomous assistant, then put several of them to work together:
- **Agent Mode**: Multi-step reasoning with tool calling, including web search, file operations, code execution, and image generation
- **Agent Squad**: Coordinate multiple specialized agents around a shared workspace, task board, and planner
- **Discussion Rooms**: Have several agents take turns in a moderated room under a turn budget, with moderated, brainstorm, round-robin, and autonomous strategies, then synthesize a conclusion and hand off execution
- **Cowork Mode**: Delegate to sub-agents with `@mention` dispatch and live activity tracking
- **Governance and Safety**: Per-agent, per-day, and per-tool spending and rate limits, policy evaluation, audit logging, and an approval workflow for sensitive actions

### Creative and Document Tools
- **Image Generation (Draw)**: Generate images with Stable Diffusion in a conversation-style interface, with a Creations gallery for editing and variations
- **Audio Transcription**: Convert speech to text locally with Whisper
- **Document Translation**: Translate PDF, DOCX, Markdown, and TXT files with glossary management

### Automation, Memory, and Sessions
- **Automations**: Schedule recurring tasks with a cron engine, templated inputs, and output actions
- **Memory System**: Namespace-based memory that auto-extracts facts from conversations and persists them across sessions
- **Sessions**: Run and route multiple inference sessions at once, each with its own model pool and lifecycle

### Extensibility: MCP, Plugins, and Connectors
- **MCP (Model Context Protocol)**: Connect to any MCP-compatible server to access databases, APIs, and custom tools through a standardized protocol
- **Plugin System**: Extend the UI and behavior with plugins built on the Plugin SDK, with UI slot injection and scoped storage
- **External Connectors**: Wire in Email (SMTP/IMAP) and Calendar (Google Calendar) with an audit log, one-click undo, and OS credential vault

### Claude Code Integration
Use Backend.AI GO as a local endpoint for Claude Code. Rewrite `claude-{haiku,sonnet,opus}-*` requests to local or cloud models with model aliases, inject live web search results (Serper, Brave, or Exa), and verify the connection with a built-in probe.

### OpenAI-Compatible API and Headless Server
Use Backend.AI GO as a local API backend for your favorite AI tools. Any application that supports the OpenAI API can connect to your locally running models. A headless server mode adds a REST API, server-sent events, and the `aigo` command-line tool, so you can run Backend.AI GO on a machine without a desktop.

### Multi-Node Mesh Networking
Scale beyond your local hardware by connecting to other Backend.AI GO instances or Backend.AI clusters. Visualize your network topology in real-time with the interactive Mesh view, and register nodes through mDNS auto-discovery, QR codes, or `aigo://` deep links.

## System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| RAM | 8 GB | 16 GB or more |
| Storage | 10 GB free | 50 GB+ (for multiple models) |
| GPU (Optional) | 4 GB VRAM | 8 GB+ VRAM |

### Platform Support

| Platform | Architecture | Notes |
|----------|--------------|-------|
| macOS | Apple Silicon (arm64) | M1/M2/M3/M4/M5 chips. Intel not supported. |
| Windows | x64 | Windows 10/11. NVIDIA GPU recommended. |
| Linux | x64, arm64 | Debian/Ubuntu (.deb), AppImage, or Flatpak |

## Installation

Download the latest version for your platform from the [Releases](../../releases) page.

| Platform | Package |
|----------|---------|
| macOS (Apple Silicon) | `backend-ai-go-x.x.x-macos-arm64.dmg` |
| Windows | `backend-ai-go-x.x.x-windows-x64-setup.exe` |
| Linux (Debian/Ubuntu) | `backend-ai-go-x.x.x-linux-x64.deb` |
| Linux (portable) | `backend-ai-go-x.x.x-linux-x64.AppImage` |
| Linux (other distros) | `backend-ai-go-x.x.x-linux-x64.flatpak` |

> Linux builds are available for both `x64` and `arm64`. For a desktop-free server, use the `aigo-server-x.x.x-linux-{x64,arm64}.deb` headless package.

### macOS (Homebrew)

```bash
brew tap lablup/tap
brew install --cask backend-ai-go
```

### macOS
1. Download the `.dmg` file
2. Open and drag Backend.AI GO to your Applications folder
3. On first launch, you may need to allow the app in **System Settings > Privacy & Security**

### Windows
1. Download and run the `.exe` installer
2. Follow the installation wizard
3. For best performance, ensure NVIDIA drivers are up to date

### Linux
```bash
# Debian/Ubuntu
sudo dpkg -i backend-ai-go-x.x.x-linux-x64.deb
sudo apt-get install -f

# AppImage (portable, no install)
chmod +x backend-ai-go-x.x.x-linux-x64.AppImage
./backend-ai-go-x.x.x-linux-x64.AppImage

# Flatpak
flatpak install backend-ai-go-x.x.x-linux-x64.flatpak
```

## Quick Start

### 1. Download a Model
- Click the **Search** icon in the sidebar
- Search for a model (e.g., `Gemma3-4B`, `Qwen3-4B`)
- Look for **GGUF** format (cross-platform) or **MLX** (macOS only)
- Click **Download** on your chosen variant (Q4_K_M recommended for balance of speed and quality)

### 2. Load the Model
- Go to the **Models** tab
- Find your downloaded model
- Click **Load** and wait for the status to show "Ready"

### 3. Start Chatting
- Click the **Chat** icon in the sidebar
- Type your message and press Enter
- Your AI responds entirely locally, no internet required

## Supported Inference Engines

Backend.AI GO integrates multiple inference engines to provide optimal performance across different hardware and use cases.

| Engine | Format | Platform | Best For |
|--------|--------|----------|----------|
| [llama.cpp](https://github.com/ggml-org/llama.cpp) | GGUF | All platforms | Cross-platform LLM inference with CPU/GPU support |
| [mlx-lm](https://github.com/ml-explore/mlx-lm) | MLX | macOS only | Maximum LLM performance on Apple Silicon |
| [stable-diffusion.cpp](https://github.com/leejet/stable-diffusion.cpp) | GGUF | All platforms | Local image generation |
| [whisper.cpp](https://github.com/ggml-org/whisper.cpp) | GGUF | All platforms | Local audio transcription |
| mlxcel | MLX | macOS only | MLX-based inference engine by Lablup, optimized for Apple Silicon (not yet public) |

## Auto-Updates

The application automatically checks for updates on startup. You can also manually check via **Settings > Check for Updates**. On Linux, the AppImage build updates in place, while deb and Flatpak installs are shown a package-manager upgrade command.

## Documentation

For detailed guides and advanced features, visit the [Backend.AI GO Documentation](https://go.backend.ai/en/manual/).

## License

Backend.AI GO is developed and maintained by [Lablup Inc.](https://www.lablup.com) as part of the [Backend.AI project](https://www.backend.ai).

## Support

We are preparing a discussion channel for bug reports and feature requests. Stay tuned for updates.
