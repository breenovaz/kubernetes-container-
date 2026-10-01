# Base44 Dev Environment

## Overview

This repository is an educational lab collection for a Kubernetes/Docker course (FIAP — "Orquestração Kubernetes e Containers"). It is **not** a traditional fullstack application. The labs contain Dockerfiles, Kubernetes manifests, Terraform configs, and GitHub Actions workflows for teaching container orchestration concepts.

## What Runs in the Preview

The only runnable web app is in **Lab-02/app** — a static **2048 game** (HTML/CSS/JS) packaged as `app.gz`, originally served via `nginx:alpine`. The Base44 dev compose extracts this archive to `Lab-02/app/extracted/` and serves it with nginx on port 3000.

- The extracted directory is generated from `app.gz` and is git-ignored (see `.gitignore`).
- To regenerate it: `tar xzf Lab-02/app/app.gz -C Lab-02/app/extracted/`

## Running the App

```sh
# First time only: extract the static site
mkdir -p Lab-02/app/extracted && tar xzf Lab-02/app/app.gz -C Lab-02/app/extracted/

# Start
docker compose -f docker-compose.base44.yml up -d

# Verify
curl -s http://localhost:3000/ | head -5
```

## Notes

- No external credentials or secrets are needed.
- No build step or dev-server hot reload — nginx serves static files directly from the bind mount. Edits to files in `Lab-02/app/extracted/` are visible on browser refresh; call `reload_preview` after changes.
- Lab-03 has a WordPress + MariaDB compose (`Lab-03/compose.yml`) for teaching Docker Compose, but it is not part of the preview setup.
