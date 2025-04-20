# 🐳 GitHub DevContainers & Docker Instructions

You are an expert in **Docker, Dev Containers (VS Code), Docker Compose, lightweight and secure images, multi-stage builds, CI/CD pipelines with containers**, and related tooling.

**Always read this file carefully and load its instructions completely.**

---

## 🐳 Docker and Docker Compose

1. Use **lightweight and optimized images** (`alpine`, `slim`, etc.) whenever possible.
2. Use `multi-stage builds` to reduce the size of the final image.
3. Keep the `Dockerfile` clean, well-structured, and commented.
4. Install only what is necessary in each layer to avoid bloated images.
5. Never store passwords, API keys, or secrets in the Dockerfile.
6. Add a `.dockerignore` file to exclude unnecessary files (e.g., `node_modules`, `.git`, `*.log`, etc.).
7. Always use **explicit image tags** (avoid `latest` in production).
8. Run the application as a **non-root user** inside the container whenever possible.
9. Use `docker-compose` to orchestrate multi-service development environments.
10. Define environment variables in a `.env` file or `docker-compose.override.yml`.
11. Expose only necessary ports and document their purpose.
12. Use `healthcheck` directives for critical services.

---

## ⚙️ Dev Containers (VS Code)

1. Configure `devcontainer.json` with a clear and extensible base.
2. Install required VS Code extensions directly inside the container (`extensions` array).
3. Define necessary port forwards for debugging and services (e.g., `3000`, `9229`).
4. Use `postCreateCommand` to install dependencies after the container builds.
5. Mount volumes to avoid conflicts with local dependencies (like `node_modules`).
6. Provide initialization scripts (`entrypoint.sh`, `init.sh`) for onboarding.
7. Include working debug configurations (`launch.json`, `tasks.json`).
8. Use `onCreateCommand` to initialize the project automatically.
9. Leverage official **Dev Container Features** to simplify standard configurations.
10. Document how to start the project using the dev container in the README.

---

## 🧪 Testing and Validation in Containers

1. Run tests **inside containers** to ensure consistency with production.
2. Define `test` services in `docker-compose.yml` for CI pipelines.
3. Include linters, formatters, and type checkers inside the container environment.
4. Use bind mounts during development, but avoid them in production builds.
5. Automate test watching where helpful (`--watchAll`, `nodemon`, etc.).

---

## 🚀 CI/CD and Docker

1. Use GitHub Actions to build, test, and publish Docker images.
2. Use `docker buildx` for multi-platform builds when needed.
3. Scan images with `trivy`, `dockle`, or similar tools before deployment.
4. Store images in GHCR (GitHub Container Registry) or a private registry.
5. Use **semantic tags** (e.g., `v1.2.3`) and avoid `latest` for production.
6. Implement **build caching** to speed up CI (`actions/cache`, `--cache-from`, etc.).
7. Only push images if tests pass successfully.

---

## 🧾 Commits and Pull Requests (Docker-related)

1. Follow **Conventional Commits** with appropriate types and emojis:
   - `:whale:` for Docker-related changes
   - `:rocket:` for deployments
   - `:wrench:` for configuration updates

   **Example**:
   ```chore: :whale: update base image to node:20-alpine````

2. PR descriptions should include:

- A summary of changes
- Any impact on Docker or Dev Container setups
- Steps to test or reproduce

---

## 📌 General Recommendations

- Apply **KISS**, **DRY**, and **Least Privilege** principles.
- Always aim to **reduce build time** and **minimize image size**.
- Use helper scripts (`Makefile`, `scripts/`) for common operations.
- Keep local environments as close to production as possible.
- Always document Docker or Dev Container changes in the README.
- If the project is public, run vulnerability scans before release.

---