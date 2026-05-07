**Here's the updated and improved documentation** that matches our current reusable workflow:

---

# 🐳 Reusable Docker Build & Push Workflow

A clean, flexible, and production-ready reusable GitHub Actions workflow for building and pushing Docker images. Supports **Docker Hub**, **GHCR**, monorepos, and multi-platform builds.

## 🚀 Features

- **Multi-Registry Support**: Docker Hub + GitHub Container Registry (GHCR)
- **Monorepo Friendly**: Configurable build context
- **Smart Tagging**: `latest`, semantic versioning, branch names, PRs
- **Multi-Platform**: `linux/amd64` + `linux/arm64` out of the box
- **Fast Builds**: GitHub Actions cache enabled
- **Secure**: Proper secret handling and minimal permissions

## 🛠 Usage Example

Create a file in your project (e.g. `POS-MVP`):

**`.github/workflows/backend-docker.yml`**

```yaml
name: Build & Push Backend

on:
  push:
    branches: [ main, master ]
    tags: [ 'v*' ]
    paths: [ 'backend/**' ]
  pull_request:
    paths: [ 'backend/**' ]

jobs:
  build-and-push:
    uses: daviekaranja/workflows/.github/workflows/build_and_push_v2.yaml@main
    with:
      image_name: pos-mvp-backend
      registry: ghcr.io                    # or docker.io
      context: backend                     # Important for monorepos
      push: ${{ github.event_name != 'pull_request' }}
      platforms: "linux/amd64,linux/arm64"
    secrets: inherit
```

---

## 📂 Inputs

| Input            | Required | Default              | Description |
|------------------|----------|----------------------|-----------|
| `image_name`     | Yes      | -                    | Name of the image (without registry) |
| `registry`       | No       | `docker.io`          | `docker.io` or `ghcr.io` |
| `context`        | No       | `.`                  | Build context path (e.g. `backend`, `frontend`) |
| `push`           | No       | `true`               | Set to `false` for PRs (build only) |
| `platforms`      | No       | `linux/amd64,linux/arm64` | Target platforms |
| `tags`           | No       | `""`                 | Additional custom tags |

---

## 🔑 Secrets

- **For GHCR** → Use `secrets: inherit` (uses `GITHUB_TOKEN` automatically)
- **For Docker Hub** → Pass these secrets:

```yaml
    secrets:
      docker_username: ${{ secrets.DOCKERHUB_USERNAME }}
      docker_password: ${{ secrets.DOCKERHUB_TOKEN }}
```

---

## 🏷 Tagging Strategy

The workflow automatically creates these tags:

- `latest` → when pushing to default branch (`main`/`master`)
- `v1.2.3` → when pushing git tags
- Branch name → e.g. `feature-new-ui`, `dev`
- PR number → for pull requests

---

## 📋 Prerequisites

1. Your `workflows` repository should be public (or the calling repo must have access).
2. For GHCR: No extra secrets needed.
3. For Docker Hub: Create a Personal Access Token with **Write** permission.

---

## ✅ Implementation Checklist

- [ ] Update reusable workflow with latest version
- [ ] Create calling workflow in target repo
- [ ] Test with a PR first (`push: false`)
- [ ] Verify image appears in GHCR or Docker Hub

---

> **Repository**: [daviekaranja/workflows](https://github.com/daviekaranja/workflows)

---
