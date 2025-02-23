# Docker Commands Reference

This document contains useful Docker commands and their descriptions, structured for easy reference.

---

## Build Commands

Build a Docker image from a Dockerfile.

```sh
docker build [OPTIONS] PATH | URL | -
```

Build an image from the current directory.

```sh
docker build .
```

Specify a Dockerfile explicitly.

```sh
docker build -f [dockerfile] .
```

Remove intermediate containers after a successful build.

```sh
docker build --force-rm=true .
```

Suppress the build cache.

```sh
docker build --no-cache .
```

Display build command help.

```sh
docker build --help
```

---

## Search & Pull Commands

Search for Docker images on Docker Hub.

```sh
docker search python
```

Filter search results for official images.

```sh
docker search --filter is-official=true python
```

Search images with at least 100 stars.

```sh
docker search --filter stars=100 python
```

Pull an image from Docker Hub.

```sh
docker image pull python
```

Pull a specific version of an image.

```sh
docker image pull python:3.12-rc-bookworm
```

Display help for the pull command.

```sh
docker image pull --help
```

---

## List Image Commands

List available Docker images.

```sh
docker image ls
```

Include all images, even intermediate ones.

```sh
docker image ls --all
```

Filter images by name.

```sh
docker image ls --filter reference=python*
```

Show detailed image information.

```sh
docker image ls --digests
```

---

## Tagging & Labeling Commands

Tag an image with a name and optional tag.

```sh
docker build -t flask-app .
```

Tag an existing image.

```sh
docker tag flask-app:v0.0.1 flask-app:v0.0.1-python
```

Label an image with metadata.

```sh
LABEL <key>=<value>
```

---

## Docker Hub Commands

Log in to Docker Hub.

```sh
docker login
```

Push an image to a repository.

```sh
docker push aleksa21000/flask-app-repo:v0.0.1
```

Pull an image from a repository.

```sh
docker pull aleksa21000/flask-app-repo:v0.0.1
```

---

## Inspect Image Commands

Get detailed metadata for an image.

```sh
docker image inspect IMAGE_ID
```

Retrieve image labels.

```sh
docker image inspect --format='{{json .Config.Labels}}' flask-app:v0.0.2
```

---

## Removing Image Commands

Remove a Docker image.

```sh
docker rmi -f flask-app:v0.0.2
```

Remove multiple images at once.

```sh
docker rmi [OPTIONS] IMAGE [IMAGE...]
```

---

## Start, Stop & Kill Commands

Start a stopped container.

```sh
docker start flask-app:v0.0.2
```

Run a new container interactively.

```sh
docker run -it -d -p 5000:5000 -v "${PWD}:/app/code" flask-app
```

Stop a running container.

```sh
docker stop flask-app:v0.0.2
```

Kill a running container.

```sh
docker kill flask-app:v0.0.2
```

---

## List Containers Commands

List currently running containers.

```sh
docker ps
```

List all containers, including stopped ones.

```sh
docker ps -a
```

List only the latest created container.

```sh
docker ps -l
```

Filter containers by exit status.

```sh
docker ps -a --filter 'exited=0'
```

---

## Common Docker Container Exit Codes

| Exit Code | Description                         |
|-----------|-------------------------------------|
| 0         | Purposely stopped                  |
| 1         | Application error                  |
| 125       | Container failed to run error      |
| 126       | Command invoke error               |
| 127       | File or directory not found        |
| 128       | Invalid argument used on exit      |
| 134       | Abnormal termination (SIGABRT)     |
| 137       | Immediate termination (SIGKILL)    |
| 139       | Segmentation fault (SIGSEGV)       |
| 143       | Graceful termination (SIGTERM)     |
| 255       | Exit Status Out Of Range           |

---

## Inspect Containers Commands

Inspect a container's metadata.

```sh
docker inspect [ID]
```

Retrieve a container's image name.

```sh
docker inspect --format='{{.Config.Image}}' [NAME|ID]
```

---

## Debugging Container Commands

View logs of a running container.

```sh
docker logs --tail 1000 -f [NAME|ID]
```

Show logs from a specific timestamp.

```sh
docker logs --since 2023-12-01T01:00:00Z [NAME|ID]
```

---

## Volume & Mounting Commands

Create a named volume.

```sh
docker volume create flask-app-vol
```

List all volumes.

```sh
docker volume ls
```

Inspect volume details.

```sh
docker volume inspect flask-app-vol
```

Run a container with a volume.

```sh
docker run -it -d -p 5000:5000 -v flask-app-vol:/app/data aleksa21000/flask-app-repo:v0.0.1
```

---

## Cleaning System Commands

Remove unused Docker images.

```sh
docker image prune -a -f
```

Remove all unused containers, networks, and volumes.

```sh
docker system prune --volumes -f
```

---

For more details, visit the [Docker documentation](https://docs.docker.com/).