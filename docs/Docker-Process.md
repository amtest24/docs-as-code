# Docker Process for Docs-as-Code

This document saves the Docker-related process used in this repository.

## What is built

- The repository is packaged into a Docker image by the Dockerfile named `docsbuilder`.
- The image contains the repo files plus the environment needed to run MkDocs.

## Build steps

1. GitHub Actions checks out the repository.
2. Docker Buildx is configured.
3. The workflow logs in to Docker Hub using GitHub secrets.
4. Docker builds the image using `docsbuilder`.
5. The image is pushed to Docker Hub with a tag like `your-username/mkdocs-docs-as-code:latest`.

## Key files

- `docsbuilder`: Dockerfile that installs Python, MkDocs, MkDocs Material, Swagger plugin, and copies the repo into the image.
- `.github/workflows/docker.yml`: GitHub Actions workflow that builds and pushes the Docker image.
- `mkdocs.yml`: MkDocs configuration used inside the container to build/serve the docs.

## How it runs

When the Docker container starts, it executes:

```bash
mkdocs serve -a 0.0.0.0:8000
```

This launches MkDocs in the container and serves the docs site on port `8000`.

## Why this is useful

- Keeps the docs build environment consistent.
- Makes it easy to run the docs site anywhere with Docker.
- Stores the built image in Docker Hub for later reuse.

## Next improvements

- Add a GitHub Pages workflow to publish static HTML if you want a live website.
- Add `mkdocs build` validation before image push.
- Improve `README.md` with Docker usage instructions.
- Keep the Docker workflow for environment testing and image distribution.
- Use GitHub Pages for actual site deployment, while Docker Hub stores the container image.
