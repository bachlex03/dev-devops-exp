# DOCKER BASIC

Description: All things you need to know as a beginner.
Reference docs: https://docs.docker.com/

## Table of Contents
- [What?](#what)
- [Where?](#where)
- [When?](#when)
- [Why?](#why)
- [How?](#how)
- [Concepts and Commands](#concepts-and-commands)
  - [Docker](#docker)
  - [Docker architecture](#docker-architecture)
  - [Docker Host & Daemon](#docker-host--daemon)
  - [Docker Client](#docker-client)
  - [Docker Registry](#docker-registry)
  - [Docker Image (concepts + CLI)](#docker-image)
  - [Docker Container (concepts + CLI)](#docker-container)
  - [Docker Volume (concepts + CLI)](#docker-volume)
  - [Docker Network (concepts + CLI)](#docker-network)
  - [Docker Compose (concepts + CLI)](#docker-compose)
  - [Docker Plugin (concepts + CLI)](#docker-plugin)
- [Optional: Pros and Cons](#optional-pros-and-cons)

## Container-Focused Quick Map
- Concepts: Docker Container, Docker Host/Daemon (runtime), Docker Volume (persistence), Docker Network (connectivity), Docker Registry (image source), Docker Image (prerequisite).
- Lifecycle CLI: `docker ps`, `docker container run|start|stop|restart|pause|unpause|rm`, `docker logs`, `docker container exec`, `docker container rename`.
- Images for containers: `docker image pull|ls|build|tag|rm`, push/pull from registry.
- Data: volumes (`docker volume create|ls|inspect|rm|prune`), bind mounts (`-v /host:/container`).
- Networking: `docker network ls|create`, attach with `--network`, publish ports with `-p`.
- Multi-container: `docker compose up|ps|logs|down`.

## What?
- Docker is a platform to build, package, and run applications in lightweight, isolated containers.

## Where?
- Supported on Linux, macOS, and Windows (via Docker Desktop/Engine).
- Images live locally in the Docker cache and remotely in registries (e.g., Docker Hub).
- Config typically lives in `Dockerfile` and `docker-compose.yml`; app code can be mounted in containers.

## When?
- Standardize environments across dev/stage/prod.
- Ship microservices and CI/CD artifacts.
- Run third-party services locally without installing them natively.

## Why?
- Consistent, repeatable runtime.
- Faster startup and lower overhead than VMs.
- Portable artifacts that run anywhere Docker is available.

## How?
- Build images from `Dockerfile`, run containers from images, persist data with volumes/bind mounts, connect services via networks, and orchestrate multi-container setups with Compose.

## Concepts and Commands

### Docker
- What: Platform providing engine, CLI, and tooling to build/run containers.
- Where: Installed on a host (local/remote) with daemon + CLI; images local cache/registries.
- When: Use to package apps into portable images and run them as containers.
- Why: Standardize runtime, isolate dependencies, and ease shipping/deployment.
- How: Write a `Dockerfile`, `docker build` an image, `docker run` a container.

### Docker architecture
- What: Client (CLI) ↔ Daemon (engine) interacting with registries, images, containers, networks, volumes.
- Where: CLI on user machine; daemon on host; registries remote; networks/volumes managed by daemon.
- When: Whenever building/pulling images and creating/running containers.
- Why: Clear separation of control plane (CLI/API) and data plane (daemon/runtime).
- How: CLI issues REST calls to daemon; daemon pulls/pushes images, creates namespaces, manages storage/network.

### Docker Host & Daemon
- What: Machine where the Docker daemon runs (local, remote, VM, or cloud instance).
- Where: Dev laptops, servers, or cloud VMs that run Docker Engine.
- When: Needed any time containers/images are built or executed.
- Why: Provides OS kernel, storage, and networking resources to containers.
- How: Install Docker Engine/Daemon on the host; CLI targets it via local socket or remote TCP.
- Daemon specifics: Background service that builds images and manages containers; listens on Unix socket/pipe or TCP; orchestrates builds, container lifecycle, networking, and volumes.

### Docker Client
- What: `docker` CLI that talks to the daemon via REST API.
- Where: Installed on user machine or inside build agents/CI runners.
- When: Used to issue commands for build/run/push/pull/manage.
- Why: Human-friendly interface to the Docker API.
- How: `docker <command>` → REST call to daemon → action executed.

#### CLI: Check version
```
docker version
```

### Docker Registry
- What: Remote store for container images (Docker Hub, ECR, GCR, Harbor, etc.).
- Where: Hosted registries on the internet or private/on-prem installs; accessed via Docker daemon/CLI over HTTPS.
- When: Use to share, version, and deploy images across teams/environments/CI-CD.
- Why: Centralizes image storage, enables reuse and distribution, supports tags and access control.
- How: `docker login`; tag local image (`docker tag LOCAL USER/IMAGE[:TAG]`); push (`docker push USER/IMAGE[:TAG]`); pull (`docker pull` or `docker run USER/IMAGE[:TAG]`).

#### CLI: Login, tag, push, pull/run
```
docker login
docker tag LOCAL_IMAGE USERNAME/IMAGE[:TAG]
docker push USERNAME/IMAGE[:TAG]
docker pull USERNAME/IMAGE[:TAG]
docker run -dp 127.0.0.1:3000:3000 USERNAME/IMAGE
```

### Docker Image
- What: Immutable, layered filesystem plus metadata; built from `Dockerfile`.
- Where: Stored locally in Docker cache and in remote registries.
- When: Built during development/CI; pulled at deploy/run time.
- Why: Provides a repeatable, portable package of an application and its dependencies.
- How: Author `Dockerfile`; `docker build`; push/pull via registry; run via `docker run`/`docker compose`.

#### CLI: Pull, list, build, tag, remove
```
docker image pull [OPTIONS] NAME[:TAG|"LATEST"]
docker image ls
docker build -t TAG_NAME[:VERSION] FOLDER_CONTAINS_DOCKERFILE
docker image rm [OPTIONS] IMAGE
docker image rmi IMAGE -f
```

### Docker Container
- What: Runtime instance of an image (isolated process with its own fs, network, resources).
- Where: Runs on the Docker Host under namespaces/cgroups, attached to networks/volumes.
- When: Started for app runtime, jobs, or services.
- Why: Provides isolation and consistent runtime from the image definition.
- How: `docker run` / `docker compose up`; manage via start/stop/exec/logs; persists data via volumes/mounts.

#### CLI: Lifecycle (list, run, stop/remove, start/restart/pause)
```
docker ps
docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]
docker run --name CUSTOM_NAME [OPTIONS] IMAGE [COMMAND] [ARG...]
docker container stop [OPTIONS] CONTAINER [CONTAINERS...]
docker container rm [OPTIONS] CONTAINER [CONTAINER...]
docker container rm -f CONTAINER
docker container start [OPTIONS] CONTAINER [CONTAINER...]
docker container pause CONTAINER [CONTAINER...]
docker container unpause CONTAINER [CONTAINER...]
docker container restart [OPTIONS] CONTAINER [CONTAINER...]
```

#### CLI: Logs, exec, rename
```
docker logs [OPTIONS] CONTAINER
docker logs -f CONTAINER
docker container exec [OPTIONS] CONTAINER COMMAND [ARG...]
docker container rename CONTAINER NEW_NAME
```

### Docker Volume
- What: Docker-managed persistent storage, decoupled from container lifecycle.
- Where: Stored under Docker’s volume store on the host.
- When: Use when data must persist beyond container lifecycle or be shared between containers.
- Why: Keeps data safe across rebuilds/restarts and avoids baking data into images.
- How: `docker volume create/list/inspect/rm`; mount with `-v volume:/path` in `docker run`/Compose.

#### CLI: Create, list, inspect, remove, prune
```
docker volume create NAME
docker volume ls
docker volume inspect NAME
docker volume rm NAME
docker volume prune
```

#### CLI: Use a named volume
```
docker run -d -p 80:80 -v log-data:/logs docker/welcome-to-docker
```

#### CLI: Bind mount (host ↔ container)
```
docker run -d -p 80:80 -v /host/path:/container/path IMAGE
```

### Docker Network
- What: Virtual network enabling container-to-container communication and port publishing.
- Where: Managed by Docker on the host (bridge/overlay/macvlan drivers, etc.).
- When: Needed for multi-container apps, service discovery, or exposing ports.
- Why: Provides isolation, name-based discovery, and controlled ingress/egress.
- How: `docker network create/list/inspect`; attach via `--network`; publish ports with `-p`.

#### CLI: List/create, attach containers, publish ports
```
docker network ls
docker network create todo-app
docker run -d --name web --network todo-app -p 8080:80 IMAGE
```

### Docker Compose
- What: Define multi-container applications declaratively with `docker-compose.yml`.
- Where: Project root containing `docker-compose.yml`.
- When: Run multi-service stacks locally or in CI; orchestrate dev/test environments.
- Why: One file to define services, networks, and volumes together.
- How: Use the `docker compose` CLI to build, start, stop, and inspect the stack.

#### CLI: Typical workflow
```
docker compose up -d
docker compose ps
docker compose logs -f
docker compose down
```

### Docker Plugin
- What: Extensions that add capabilities (volumes, networks, logging, etc.).
- Where: Installed on the Docker Host and managed by the daemon.
- When: Use when built-in drivers/features are insufficient.
- Why: Extend Docker with custom storage/network/logging behaviors.
- How: `docker plugin install/ls/enable/disable/rm`; configure per plugin instructions.

#### CLI: Manage plugins
```
docker plugin ls
docker plugin install NAME
docker plugin enable NAME
docker plugin disable NAME
docker plugin rm NAME
```

#### CLI: Build, run specific services, view config
```
docker compose build
docker compose up -d SERVICE_NAME
docker compose exec SERVICE_NAME COMMAND
docker compose config
```

## Optional: Pros and Cons
Pros
- Fast, consistent environments across machines.
- Lightweight compared to virtual machines.
- Strong ecosystem (registries, Compose, orchestration).

Cons
- Learning curve around networking, volumes, and security.
- Requires daemon/engine; some OS-specific constraints.
- Containers share the host kernel, so isolation is not as strong as VMs.

## Common Flows

1. Write Dockerfile
2. Build image from Dockerfile
3. Tag image with version
4. Write docker compose
5. Push to docker registry (Docker hub)

