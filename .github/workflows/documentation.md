# 🐳 Reusable Docker Build Workflow

A professional-grade, reusable GitHub Action for building and pushing Docker images to Docker Hub. Designed for Python/FastAPI projects, monorepos, and multi-environment tagging strategies.

## 🚀 Features

- **Smart Tagging**: Automatically handles `latest`, Semantic Versioning (`v1.0.0`), and branch-based tags (`dev`, `feature-x`).
- **Monorepo Support**: Configurable build context and Dockerfile paths.
- **Performance**: Implements GitHub Actions (GHA) caching to speed up builds by up to 80%.
- **Multi-Platform Ready**: Includes QEMU setup for cross-platform image compatibility.

## 📋 Prerequisites

- **Secrets**: You must define `DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN` in your repository or organization secrets.
- **Repo Access**: Ensure your workflows repository is public or shared within your GitHub Organization.

## 🛠 Usage Example

Create a file at `.github/workflows/deploy.yml` in your application repository:

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [main, dev]
    tags: ['v*']

jobs:
  docker-build:
    uses: <your-username>/workflows/.github/workflows/docker-build-push.yml@main
    with:
      image_name: "fastapi-service"
      build_context: "."           # Default
      dockerfile_path: "Dockerfile" # Default
    secrets: inherit
```

## 📂 Inputs & Secrets

### Inputs

| Input           | Required | Default      | Description                        |
| --------------- | -------- | ------------ | ---------------------------------- |
| `image_name`    | Yes      | N/A          | The name for the Docker Hub image. |
| `build_context` | No       | `.`          | Folder scope for the Docker build. |
| `dockerfile_path` | No       | `./Dockerfile` | Path to the Dockerfile.            |

### Secrets

| Secret             | Required | Description                                  |
| ------------------ | -------- | -------------------------------------------- |
| `DOCKERHUB_USERNAME` | Yes      | Your Docker Hub ID.                          |
| `DOCKERHUB_TOKEN`    | Yes      | A Personal Access Token (PAT) from Docker Hub. |

## 🏷 Tagging Logic

- **Push to `main` branch**: Pushes `image:latest`.
- **Push a Tag (`v1.2.3`)**: Pushes `image:1.2.3`.
- **Push to `dev` branch**: Pushes `image:dev`.
- **Push to any other branch**: Pushes `image:<branch-name>`.

## ✅ Implementation Checklist

- **Docker Hub PAT**: Don't use your Docker Hub password; generate a Token in Docker Hub Account Settings for better security.

---

 > Thanks for using this reusable workflow! If you have any questions or need further assistance, feel free to open an issue or contribute to the repository. Happy coding! 🚀
