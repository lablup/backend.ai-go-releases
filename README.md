# Backend.AI GO

**Run AI models locally on your desktop — private, fast, and fully under your control.**

Backend.AI GO is a cross-platform desktop application that lets you run Large Language Models (LLMs) directly on your machine. Download models from Hugging Face, chat with AI privately, connect to cloud providers, or scale to other Backend.AI GO instances and enterprise clusters when you need more power.

## Key Features

### Local AI Inference
Run popular models like Gemma 3, Qwen3, Llama, and Mistral entirely on your hardware. Your conversations stay on your machine — no data leaves your computer.

### Hardware Acceleration
- **Apple Silicon (MLX)**: Native acceleration for M1/M2/M3/M4/M5 chips
- **NVIDIA GPU (CUDA)**: Full GPU acceleration on Windows and Linux
- **AMD GPU (HIP/ROCm)**: Support for AMD graphics cards
- **Intel GPU (SYCL)**: Acceleration for Intel Arc and Iris graphics
- **CPU**: Optimized inference for systems without dedicated GPUs

### Hybrid Cloud Integration
Seamlessly combine local models with cloud APIs. Use local models for sensitive data, switch to GPT, Claude, or Gemini for complex tasks — all from the same interface.

Supported providers:
- OpenAI (GPT-5.2, GPT Image 1.5, etc.)
- Anthropic (Claude 4.5 Sonnet, Claude 4.5 Opus)
- Google (Gemini 3 Pro, Gemini 3 Flash)
- Any OpenAI-compatible endpoint (Ollama, LocalAI, vLLM, etc.)

### Agent Mode with Tool Calling
Transform your AI from a simple chatbot into an autonomous assistant:
- **Web Search**: Get real-time information from the internet
- **File Operations**: Read, analyze, and manage local files
- **Code Execution**: Run Python scripts and shell commands
- **Calculator**: Perform precise mathematical calculations

### MCP (Model Context Protocol) Support
Connect to any MCP-compatible server to extend your AI's capabilities. Access databases, APIs, and custom tools through a standardized protocol.

### OpenAI-Compatible API Server
Use Backend.AI GO as a local API backend for your favorite AI tools. Any application that supports the OpenAI API can connect to your locally running models.

### Multi-Node Mesh Networking
Scale beyond your local hardware by connecting to other Backend.AI GO instances or Backend.AI clusters. Visualize your network topology in real-time with the interactive Mesh view.

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
| Linux | x64 | Ubuntu/Debian (.deb) or Flatpak |

## Installation

Download the latest version for your platform from the [Releases](../../releases) page.

| Platform | Package |
|----------|---------|
| macOS (Apple Silicon) | `backend.ai-go-x.x.x-macos-arm64.dmg` |
| Windows | `backend.ai-go-x.x.x-windows-x64-setup.exe` |
| Linux (Debian/Ubuntu) | `backend-ai-go-x.x.x-linux-x64.deb` |
| Linux (Other distros) | `backend-ai-go-x.x.x-linux-x64.flatpak` |

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
- Your AI responds entirely locally — no internet required

## Supported Inference Engines

Backend.AI GO integrates multiple inference engines to provide optimal performance across different hardware and use cases.

| Engine | Format | Platform | Best For |
|--------|--------|----------|----------|
| [llama.cpp](https://github.com/ggerganov/llama.cpp) | GGUF | All platforms | Cross-platform LLM inference with CPU/GPU support |
| [mlx-lm](https://github.com/ml-explore/mlx-lm) | MLX | macOS only | Maximum LLM performance on Apple Silicon |
| [stable-diffusion.cpp](https://github.com/leejet/stable-diffusion.cpp) | GGUF | All platforms | Local image generation |
| mlxcel | MLX | macOS only | Experimental MLX-based inference engine by Lablup (not yet public) |

## Auto-Updates

The application automatically checks for updates on startup. You can also manually check via **Settings > Check for Updates**.

## Documentation

For detailed guides and advanced features, visit the [Backend.AI GO Documentation](https://go.backend.ai/en/manual/).

## License

Backend.AI GO is developed and maintained by [Lablup Inc.](https://www.lablup.com) as part of the [Backend.AI project](https://www.backend.ai).

## Support

We are preparing a discussion channel for bug reports and feature requests. Stay tuned for updates.
