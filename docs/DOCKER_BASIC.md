# DOCKER BASIC

Description: All things need to know for beginner
Refernce docs: https://docs.docker.com/

## Concepts

### Docker

### Docker architecture

### Docker Host

#### Docker Daemon (child concept in Docker Host)

### Docker Docker Client

### Docker Registry

### Docker Image


### Docker Container

### Docker Volume

### Docker Network

### Docker Plugin


## Docker CLI

### Check version

```
docker -version
```

### Pull image

```
docker image pull [OPTIONS] NAME[:TAG|"LATEST"]
```


### List/Remove images

```
docker image ls
docker images // alias

docker image rm [OPTIONS] IMAGE [IMAGE...]
docker image rmi IMAGE [alias]
docker image rmi IMAGE -f
```

### Build (Dockerize/Containerize/Spin Up/Create) images

note: enable docker engine

```
docker build -t TAG_NAME FOLDER_CONTAINS_DOCKERFILE
```

### Tag(Image version) image

build + tag + version
```
docker build -t TAG_NAME[:VERSION] FOLDER_CONTAINS_DOCKERFILE
```

### List/Run/Stop/Remove container from an image

```
docker ps

docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]

docker container stop [OPTIONS] CONTAINER [CONTAINERS...]

docker contaner rm [OPTIONS] CONTAINER [CONTAINER...]
docker contaner rm -f CONTAINER [CONTAINER...] //force remove (no need to stop container)
```

### Start/Pause/Unpause/Restart container


```
docker container start [OPTIONS] CONTAINER [CONTAINER...]

docker container pause CONTAINER [CONTAINER...]

docker container unpause CONTAINER [CONTAINER...]
docker container restart [OPTIONS] CONTAINER [CONTAINER...]
```

### Get logs in container

```
docker logs [OPTIONS] CONTAINER

docker logs -f CONTAINER
```

### Rename container

```
docker container rename CONTAINER NEW_NAME
```

### Exec command

```
docker container exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

### Push docker image to docker registry (docker hub)

step-by-step:
1. docker login
2. docker tag with format `USERNAME/IMAGE`
3. push ("latest" as default tag)

```

```

### Pull and run image from docker registry

```
docker run -dp 127.0.0.1:3000:3000 USERNAME/IMAGE
```

### Share local files to container

```

```

## Docker volumn

### Persit container data

Methods:
- Volumes
- Bind mount

```
docker run -d -p 80:80 -v log-data/logs docker/welcome-to-docker
```

### Create volume

```
docker volume create log-data
```

### List volumes

```
docker volume ls
```

### Inspect volume

```
docker volume inspect VOLUME
```

### Remove volume

```
docker volume rm VOLUME
```

### Remove all unused (unattached) volumes

```
docker volume prune
```

### Bind mount

Description: mount local file system to container file system

## Docker network

Description: Multi Container Apps with network

### List network

```
docker network ls
```

### Create docker network

```
docker network create todo-app
```

### Run container with network

```

```

## Docker compose


