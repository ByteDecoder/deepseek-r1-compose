# LLM Local Deployment with Docker, Ollama & Open WebUI

![Deepseek-R1 Web UI Screenshot](article1.jpg)

This project provides a ready-to-use Docker Compose setup for running the DeepSeek-R1 language model locally, along with a simple web-based user interface.

## Features

- **Local LLM Inference:** Run DeepSeek-R1 models on your own hardware using [Ollama](https://ollama.com/).
- **Web UI:** Interact with the model via a browser-based interface in the `web/` directory.
- **Easy Model Management:** Pull and manage model versions with Docker commands.

## Quick Start

1. **Start the Ollama Service**

```bash
docker compose up -d

# Pull LLM
# Installing DeepSeekR1:1.5B and other LLM's
docker exec ollama ollama pull deepseek-r1:1.5b
docker exec ollama ollama pull deepseek-r1:7b
docker exec ollama ollama pull deepseek-coder:1.3b
docker exec ollama ollama pull llama3.2:3b
docker exec ollama ollama pull gemma2:9b
docker exec ollama ollama pull mistral:7b
```

Check NVIDIA

```bash
docker exec -it ollama nvidia-smi
```

Check if GPU is doing work:

```bash
docker exec -it ollama ollama ps
```

## Recommended Models for a NVIDIA RTX 6GB 3060

| Model | Size | Speed on your 3060 |
|-------|------|-------------------|
| Llama 3.2 (3B) | ~2.0GB | Blazing Fast (Full GPU) |
| Mistral (7B) | ~4.1GB | Fast (Full GPU) |
| Llama 3.1 (8B) | ~4.7GB | Fast (Full GPU) |
| Gemma 2 (9B) | ~5.4GB | Good (Likely Full GPU) |
| Command R | 20GB+ | Slow (Mostly CPU/RAM) |

1. **Pull the DeepSeek-R1 Model**

   Choose your desired model size (e.g., `1.5b`):

   ```bash
   docker compose exec ollama ollama pull deepseek-r1:1.5b
   ```

2. **Access the Web UI**

   - Custom UI <http://localhost:6001>
   - Open WebUI <http://localhost:6002>

   Open <http://localhost:6002> in your browser to interact with the model.

3. Add new models

   ```bash
   docker compose exec ollama ollama pull deepseek-r1:7b
   docker compose exec ollama ollama pull deepseek-coder:1.3b
   ```

   Inside the Ollama container

   ```bash
   ollama pull  phi3:mini
   ollama pull qwen3:1.7b
   ollama pull mistral
   ```

## Project Structure

```bash
.
├── docker-compose.yml         # Docker Compose configuration for Ollama
├── ollama-models/             # Model storage (keys, manifests, blobs)
│   ├── id_ed25519
│   ├── id_ed25519.pub
│   └── models/
│       ├── blobs/             # Model weights and data
│       └── manifests/         # Model manifests
├── web/                       # Web UI files
│   ├── index.html
│   ├── ollama.js
│   ├── showdown.min.js
│   └── style.css
└── README.md                  # Project documentation
```

## Notes

- Model files are stored in `ollama-models/`. You can add or remove models as needed.
- The web UI is static and communicates with the Ollama backend.
- For advanced configuration, edit [docker-compose.yml](docker-compose.yml).

## Troubleshoting

- Check Ollama  is runing on <http://localhost:11434>
- Custom Web UI is running on <http://localhost:6001>
- Open Web UI is running on <http://localhost:6002>

## References

- [Ollama Documentation](https://github.com/jmorganca/ollama)
- [DeepSeek-R1 Model Card](https://huggingface.co/deepseek-ai/DeepSeek-R1)
- <https://dev.to/savvasstephnds/run-deepseek-locally-using-docker-2pdm>
- <https://platzi.com/blog/deepseek-r1-instalar-local/>
- <https://www.composerize.com/>

---
