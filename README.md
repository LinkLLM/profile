<div align="center">

<img src="https://img.shields.io/badge/LinkLLM-Local%20AI%20Inference-0F172A?style=for-the-badge&logoColor=white" alt="LinkLLM" />

# ⚡ LinkLLM

### High-Performance Local LLM Inference Server

**OpenAI-Compatible · Rust-Native · Built for Developers**

<br/>

[![License](https://img.shields.io/badge/License-Apache%202.0-blue?style=flat-square)](LICENSE)
[![Language](https://img.shields.io/badge/Language-Rust-orange?style=flat-square&logo=rust)](https://www.rust-lang.org/)
[![API](https://img.shields.io/badge/API-OpenAI%20Compatible-412991?style=flat-square&logo=openai)](https://platform.openai.com/docs/api-reference)
[![Status](https://img.shields.io/badge/Status-In%20Development-yellow?style=flat-square)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen?style=flat-square)](CONTRIBUTING.md)

<br/>

[Overview](#-overview) · [Features](#-features) · [Quick Start](#-quick-start) · [API Reference](#-api-reference) · [Roadmap](#-roadmap) · [Contributing](#-contributing)

---

</div>

## 📌 Overview

**LinkLLM** is a blazing-fast, local LLM inference server written in **Rust** — designed to be a drop-in replacement for the OpenAI API on your own hardware. Run open-source language models privately, without cloud costs, without data leaving your machine.

Whether you're building AI-powered applications, experimenting with open-source models, or running production inference on-premise — LinkLLM gives you the speed, control, and compatibility you need.

```
Your App  →  OpenAI SDK  →  LinkLLM Server  →  Local Model
                               (localhost)       (no cloud)
```

> **Vision:** Make local LLM inference as simple as a single command — fast enough for production, open enough for everyone.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔌 **OpenAI-Compatible API** | Drop-in replacement — works with any OpenAI SDK out of the box |
| ⚡ **Rust-Native Performance** | Memory-safe, zero-cost abstractions, minimal latency overhead |
| 🏠 **100% Local** | Your data stays on your machine — no telemetry, no cloud calls |
| 📦 **Multi-Format Support** | Run models in GGUF, safetensors, and other popular formats |
| 🔧 **Developer First** | Clean configuration, detailed logging, easy integration |
| 🌐 **Cross-Platform** | Linux, macOS, Windows support |
| 🆓 **Open Source** | Apache 2.0 — free to use, modify, and distribute |

---

## 🚀 Quick Start

### Prerequisites

- Rust `1.75+` ([Install Rust](https://rustup.rs/))
- A compatible model file (GGUF recommended for CE)

### Installation

```bash
# Clone the repository
git clone https://github.com/LinkLLM/linkllm.git
cd linkllm

# Build in release mode
cargo build --release

# Run the server
./target/release/linkllm --model ./models/your-model.gguf --port 8080
```

### Test It

```bash
curl http://localhost:8080/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "local-model",
    "messages": [{"role": "user", "content": "Hello, LinkLLM!"}]
  }'
```

### Use with OpenAI SDK (Python)

```python
from openai import OpenAI

client = OpenAI(
    base_url="http://localhost:8080/v1",
    api_key="not-needed"  # LinkLLM doesn't require a key locally
)

response = client.chat.completions.create(
    model="local-model",
    messages=[{"role": "user", "content": "Explain what LinkLLM does."}]
)

print(response.choices[0].message.content)
```

---

## 📡 API Reference

LinkLLM implements the OpenAI REST API spec. Supported endpoints:

| Endpoint | Method | Status |
|---|---|---|
| `/v1/chat/completions` | `POST` | ✅ Supported |
| `/v1/completions` | `POST` | ✅ Supported |
| `/v1/models` | `GET` | ✅ Supported |
| `/v1/embeddings` | `POST` | 🔄 Planned |

Full API documentation → [`/docs`](docs/)

---

## 🗂️ Repository Structure

```
LinkLLM/
├── linkllm/              # Core inference server (Rust)
├── linkllm-py/           # Python client SDK (planned)
├── linkllm-node/         # Node.js client SDK (planned)
├── linkllm-docs/         # Documentation site
└── linkllm-models/       # Model configs & quantization guides
```

---

## 🗺️ Roadmap

### Phase 1 — Community Edition (CE) `v0.1.0`
- [x] Project architecture & core design
- [ ] GGUF model loading via `llama.cpp` bindings
- [ ] OpenAI-compatible `/v1/chat/completions` endpoint
- [ ] Basic CLI configuration
- [ ] Apache 2.0 open-source release

### Phase 2 — Stability & Ecosystem `v0.2.0`
- [ ] Safetensors format support
- [ ] Streaming responses (SSE)
- [ ] Multi-model routing
- [ ] Python & Node.js SDK wrappers
- [ ] Docker image

### Phase 3 — Advanced Features `v1.0.0`
- [ ] GPU acceleration (CUDA / Metal)
- [ ] Batched inference
- [ ] Context caching
- [ ] Web UI dashboard
- [ ] LinkLLM Cloud (SaaS tier)

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────┐
│              LinkLLM Server             │
│                                         │
│  ┌──────────┐    ┌────────────────────┐ │
│  │  HTTP    │    │   Model Manager    │ │
│  │  Layer   │───▶│  (GGUF / ST / ...) │ │
│  │ (Axum)   │    └────────────────────┘ │
│  └──────────┘             │             │
│       │              ┌────▼───────────┐ │
│  OpenAI API     │   │ Inference Core │ │
│  Compatible     │   │  (Rust-native) │ │
│                      └────────────────┘ │
└─────────────────────────────────────────┘
```

**Core stack:** Rust · [Axum](https://github.com/tokio-rs/axum) · [Tokio](https://tokio.rs/) · [llama.cpp bindings](https://github.com/ggerganov/llama.cpp)

---

## 🤝 Contributing

LinkLLM is built in public. Contributions, issues, and feedback are welcome.

1. Fork the repository
2. Create your branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'feat: add amazing feature'`
4. Push and open a Pull Request

Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting a PR.

---

## 📄 License

LinkLLM Community Edition is released under the **Apache License 2.0**.
See [LICENSE](LICENSE) for full details.

---

<div align="center">

**Built with ❤️ by [AJ Ashik](https://github.com/theajashik) and the LinkLLM community**

*Making local AI inference accessible to every developer.*

<br/>

⭐ **Star this repo if you find it useful** ⭐

</div>
