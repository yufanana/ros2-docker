# Template for running ROS2 projects in docker containers

Based on [Sebastion Castro's blogpost](https://roboticseabass.com/2023/07/09/updated-guide-docker-and-ros2/).

## Background

- Source image: pre-built public images
  - Ubuntu 22.04
  - ROS 2 distro with desktop tools
- Base image: dependencies
  - apt
  - Python
  - ROS packages to install from binary (e.g. TurtleBot3)
- Overlay image: source code that will not be modified
- Dev container: project source code for development

Entrypoints are used to automatically source workspaces and set environment variables.

## Installation

1. Install [Docker](https://docs.docker.com/engine/install/).

2. Configure project name in `.env`.

3. Configure `ROS_DISTRO` in `docker/Dockerfile`

4. Build container.

```bash
cd ros2-docker
docker compose --file docker-compose.yaml --env-file .env build
```

5. Run container.

```bash
# In one terminal,
cd ros2-docker && docker compose up

# In subsequent terminals,
docker exec -it <container-name>-dev bash
```

## Development

Place the project's source code in `ros2-docer/src` as this is a mounted volume that are only available at runtime.
