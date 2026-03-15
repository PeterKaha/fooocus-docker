# Fooocus Docker Setup

A simple Docker setup for [Fooocus](https://github.com/lllyasviel/Fooocus), an AI-based image generator. Focused on prompting and generating with Stable Diffusion. Uses the official pre-built image – no custom building required.

## Prerequisites

- Docker and Docker Compose
- NVIDIA GPU (for CUDA support) – optional, but recommended for better performance
- At least 8 GB RAM, 16 GB recommended

## Installation and Start

1. **Clone or download the repository:**
   ```bash
   git clone https://github.com/PeterKaha/fooocus-docker.git
   cd fooocus-docker
   ```

2. **Start the container:**
   ```bash
   docker compose up -d
   ```
   This automatically pulls the image `ghcr.io/lllyasviel/fooocus` and starts Fooocus.

3. **Open Fooocus:**
   - Open http://localhost:7865 in the browser.
   - The web UI automatically loads the available models.

## Adding Models

Fooocus uses local models from the `models/` folder. Add new models:

- **Checkpoints** (main models): Place in `models/checkpoints/` (e.g., `.safetensors` files)
- **LoRAs**: Place in `models/loras/`
- **Embeddings**: Place in `models/embeddings/`
- **Others**: See `config.txt` for paths

After adding, restart the container:
```bash
docker compose down
docker compose up -d
```

## Directory Structure

```
fooocus-docker/
├── docker-compose.yml    # Container configuration
├── fooocus/
│   └── config.txt        # Path configuration for models
├── models/               # Local models (mounted in container)
│   ├── checkpoints/      # Main models
│   ├── loras/            # LoRA adapters
│   └── ...               # Other folders
├── fooocus-outputs/      # Generated images (mounted)
└── .gitignore            # Ignores models and outputs for Git
```

## Configuration

- **GPU**: Automatically detected if available.
- **Ports**: Default port 7865.
- **Volumes**:
  - `models/` for models
  - `fooocus-outputs/` for outputs
  - `fooocus-data` (named volume) for persistent data

## Troubleshooting

- **Container not starting?** Check GPU drivers and Docker setup.
- **Models not visible?** Ensure files are in the correct folders and container is restarted.
- **Check logs:** `docker compose logs`
