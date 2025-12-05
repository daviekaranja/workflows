---

# 📄 README.md

## Workflows Repository

This repository contains a collection of **reusable GitHub Actions workflows** designed to be shared across multiple projects. By centralizing CI/CD logic here, you can keep individual repositories clean, consistent, and easy to maintain.

All workflows in this repo utilize **`workflow_call`**, allowing any other repository to invoke them without duplicating YAML files.

---

## 🚀 Purpose

This repository serves as a dedicated hub for:

- Common CI tasks (lint, type-check, test)
- Build processes (Node.js, frontend frameworks, backend code, etc.)
- Docker operations (build, tag, publish)
- Deployment steps (platform-specific, cloud, or server deployments)
- Any automation that should be reused across multiple repositories

**Benefits:**
- All workflow updates are applied globally—no need to edit each project separately.
- Ensures consistent CI/CD practices across your organization.

---

## 📁 Repository Structure

All reusable workflows are stored under:

```
.github/workflows/
```

Each workflow is a standalone `.yml` file and can be referenced by other repositories.

<details>
<summary>Example Structure</summary>

```
.github/
└── workflows/
    ├── lint.yml
    ├── build.yml
    ├── docker.yml
    ├── deploy.yml
    └── ...
```
</details>

You can add as many workflow files as your ecosystem requires.

---

## 🧩 How to Use These Workflows in Other Repositories

Any GitHub repository can call a workflow from this repository using the following syntax:

```yaml
jobs:
  my_job_name:
    uses: <your-username-or-org>/workflows/.github/workflows/<workflow-file>.yml@main
```

**Replace:**
- `<your-username-or-org>`: your GitHub username or organization name
- `<workflow-file>`: the desired workflow file (e.g., `build.yml`)
- `@main`: the branch or tag to reference (see [🌐 Versioning](#versioning) below)

### Example:

```yaml
jobs:
  ci:
    uses: your-org/workflows/.github/workflows/build.yml@main
    with:
      # workflow inputs here
    secrets:
      # workflow secrets here
```
**Note:** Fill in the `with:` block for the workflow's required inputs, and the `secrets:` block for any secrets.

---

## 🔧 Inputs and Secrets

**Inputs:**  
Parameters passed under the `with:` block to customize workflow behavior (such as Node version, working directory, Docker image name, deployment environment, etc).

**Secrets:**  
Sensitive values passed under the `secrets:` block.
- **Secrets are not stored here**, but in the calling repository.
- This maintains security while allowing workflows to use required credentials or tokens.

---

## 🌐 Versioning

To avoid disrupting dependent repositories:

- **Branch Reference** (e.g. `@main`): Get the latest workflow updates immediately.
- **Tag Reference** (e.g. `@v1`): Pin to a stable, predictable version.

**Recommendation:**  
Use a tag for production/dependant projects and follow `main` for the latest features in development.

---

## 🛠️ Why This Repo Exists

- Centralizes workflow logic for easy management
- Maintains standardized CI/CD patterns across projects
- Reduces duplication in application repositories
- Ensures consistent tooling and configuration
- Makes adding, updating, or debugging automations much simpler

As your ecosystem grows, this repository becomes the single source of truth for all automation.

---

## 📌 Contributing

If you'd like to add or update a workflow:

1. Create a new file in `.github/workflows/`.
2. Define your workflow using `workflow_call` for reusability.
3. Document your workflow’s inputs and secrets *inside the workflow file*.
4. Push your changes and update any dependent repositories as needed.

---
