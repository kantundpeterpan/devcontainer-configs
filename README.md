# DevContainer Configs

This repository contains reusable devcontainer configurations with **DevPod prebuild support** and **uv Python package manager**. Can be used as a git submodule or standalone.

## Key Features

✅ **DevPod Prebuilds** - Built-in support with customizable repository
✅ **uv Package Manager** - Fast Python dependency management
✅ **Docker-in-Docker** - Full Docker CLI support in all variants
✅ **Cloud Integration** - GCP authentication and tools
✅ **Multiple Variants** - Fullstack, Data Science, GEN-AI

## Usage

### Option 1: As a Git Submodule (Recommended)

```bash
# Add as submodule to your project
git submodule add https://github.com/yourusername/devcontainer-configs.git .devcontainer

# Create your project-specific devcontainer.json
cat > devcontainer.json << EOF
{
  "extends": "./.devcontainer/fullstack/devcontainer.json",
  "name": "My Project",
  "customizations": {
    "vscode": {
      "extensions": ["project-specific-extension"]
    },
    "devpod": {
      "prebuildRepository": "ghcr.io/myorg/myproject-devpod"
    }
  }
}
EOF
```

### Option 2: Direct Image Reference

```json
{
  "image": "ghcr.io/yourusername/devcontainer-base-images/fullstack:latest",
  "customizations": {
    "vscode": {
      "extensions": ["ms-python.python"]
    },
    "devpod": {
      "prebuildRepository": "ghcr.io/myorg/myproject-devpod"
    }
  }
}
```

## Available Configurations

### 1. Fullstack Configuration
**Base Image**: `ghcr.io/yourusername/devcontainer-base-images/fullstack:latest`

- Python 3.11 + uv package manager
- Node.js LTS
- Google Cloud SDK
- Docker CLI + Docker-in-Docker
- GitHub Actions (act)
- VS Code extensions: Python, Pylance, Ruff, GitHub Actions, Gemini CLI

### 2. Data Science Configuration
**Base Image**: `ghcr.io/yourusername/devcontainer-base-images/datascience:latest`

- Python 3.13 + uv
- Jupyter Lab with extensions
- pandas, numpy, matplotlib, scikit-learn, seaborn, plotly
- Docker CLI
- VS Code extensions: Python, Pylance, Jupyter tools

### 3. Data Science Extended Configuration
**Base Image**: `ghcr.io/yourusername/devcontainer-base-images/datascience-extended:latest`

- Python 3.13 + uv
- Jupyter Lab with extensions
- pandas, numpy, matplotlib, scikit-learn, seaborn, plotly
- **Polars** - High-performance DataFrames
- **SQLAlchemy** - SQL toolkit and ORM
- **SQLite** - Embedded database
- **XGBoost, LightGBM, CatBoost** - Gradient boosting
- **Optuna** - Hyperparameter optimization
- **Great Expectations** - Data validation
- Docker CLI
- VS Code extensions: Python, Pylance, Jupyter tools, SQLTools

### 4. GEN-AI Chainlit Configuration
**Base Image**: `ghcr.io/yourusername/devcontainer-base-images/genai-chainlit:latest`

- Python 3.11 + uv
- Chainlit + LangChain + LangGraph
- transformers + sentence-transformers + faiss-cpu
- Docker CLI
- VS Code extensions: Python, Pylance, Chainlit

### 5. Showcase Configuration
**Base Image**: `ghcr.io/yourusername/devcontainer-base-images/fullstack:latest`

- Auto-starting services (frontend + backend)
- Port forwarding: 8000 (backend), 5173 (frontend)
- GCP authentication support
- Generic startup script template
- Continue extension for AI assistance

## DevPod Prebuilds

All configurations include built-in DevPod prebuild support. The prebuild repository can be customized:

```json
{
  "extends": "./.devcontainer/fullstack/devcontainer.json",
  "customizations": {
    "devpod": {
      "prebuildRepository": "${localEnv:DEVPOD_PREBUILD_REPO}"
    }
  }
}
```

**Environment Variables**:
- `DEVPOD_PREBUILD_REPO`: Custom prebuild repository (default: `ghcr.io/yourusername/devpod-cache`)
- `GCP_SA_KEY`: Google Cloud service account key for authentication

## Showcase Variant

The showcase configuration includes a generic startup script template with:

1. **GCP Authentication**: Automatic service account setup
2. **Frontend Setup**: npm install and environment configuration
3. **Backend Startup**: Python server with auto-reload
4. **Port Waiting**: Intelligent port detection
5. **Codespaces Support**: Automatic URL configuration

### Using the Showcase Template

1. Copy the template:
```bash
cp .devcontainer/showcase/startup.sh.template .devcontainer/showcase/startup.sh
```

2. Edit paths to match your project structure
3. Reference in devcontainer.json:
```json
{
  "extends": "./.devcontainer/showcase/devcontainer.json"
}
```

## Customization

### Overriding Settings

```json
{
  "extends": "./.devcontainer/fullstack/devcontainer.json",
  "name": "My Custom Project",
  "forwardPorts": [3000, 8000],
  "customizations": {
    "vscode": {
      "extensions": ["additional-extension"]
    },
    "devpod": {
      "prebuildRepository": "ghcr.io/myorg/custom-devpod"
    }
  }
}
```

### Adding Project-Specific Features

```json
{
  "extends": "./.devcontainer/fullstack/devcontainer.json",
  "features": {
    "ghcr.io/devcontainers/features/postgresql:1": {
      "version": "14"
    }
  }
}
```

## SSH Key Mounting

All configurations include SSH key mounting for seamless Git operations:

```json
"mounts": [
  "source=${localEnv:HOME}/.ssh,target=/home/vscode/.ssh,type=bind,consistency=cached"
]
```

## Environment Variables

- `GCP_SERVICE_ACCOUNT_KEY`: Google Cloud service account key
- `DEVPOD_PREBUILD_REPO`: Custom DevPod prebuild repository
- `CODESPACE_NAME`: Automatically detected in GitHub Codespaces

## License

MIT License. See LICENSE file for details.