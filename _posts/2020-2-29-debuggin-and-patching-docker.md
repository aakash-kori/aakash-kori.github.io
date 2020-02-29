---
title: "My Notes: Debugging And Patching Docker"
category: "notes"
tags: ["patching", "debugging", "docker"]
desc: This article provide some notes for debugging and patching docker.
poster: working-with-container.jpg
---

Containerization of software and services allows easy deployment, portability and many other benefits. Docker is one of wide-spread adopted technology used for containerization. I use docker while on work. There are many guide and articles about using and debugging docker. Here is my guide for debugging and patching docker. And link to [resources](#Resources).

# Terminologies

- docker - software used for containerization.
- image - snapshot of container.
- container - running instance of image.

# Information Gathering

The first stage of any debugging session is gathering information. Skipping this steps may lead to spending hours on issue which may have been resolved in minutes.

## Container inspect

- List all running container. 

  ```bash
  docker ps
  ```

- List all containers (running, created, exited, ...).

  ```bash
  docker ps -a
  ```

- List container based on filter (say status=exited).

  ```bash
  docker ps -a -f "status=exited"
  ```

- Get container logs.

  ```bash
  docker logs "$container_name"
  ```

- Get more information on the container.

  ```bash
  docker container inspect "$container_name"
  ```

## Images inspect

- List all docker images.

  ```bash
  docker images
  ```

- Get more information on the image. 

  ```bash
  docker image inspect "$image_name":"$image_tag"
  ```

## Format output into json

- Get names of exited container.

  {% raw %}

  ```bash
  docker ps -a -f "status=exited" --format "{{json .Names}}"
  ```

  {% endraw %}

# Live Debugging

Once information is gathered, we may need to tweak the container or live-debug. Most of these cases may require us to get shell on the docker. The method of getting shell may differ based on weather docker is running or docker has exited.

## Docker is running

- Exec into the shell (bash or sh or other shell).

  ```bash
  docker exec -it "$container_name" /bin/sh
  ```

- Run command `ls .`.

  ```bash
  docker exec -t "$container_name" ls .
  ```

## Docker has exited

- Get image, tag pair for exited container.

  {% raw %}

  ```bash
  docker ps -f "name=$container_name" --format "{{json .Image}}"
  ```

  {% endraw %}

- Run image to get shell.

  ```bash
  docker run -it --entrypoint sh "$image_name":"$image_tag"
  ```

- Run command `ls .`.

  ```bash
  docker run -it --entrypoint ls "$image_name":"$image_tag" .
  ```

# Post Debugging

After figuring out the issue, You may want to patch the environment or rollback and also do some basic cleanup. Rollback would be to tag previous tag to latest. In case previous tag is not available (as it is first deployment) or the version has some specific changes which cannot be reverted and patch release may take time, there is need to patch the docker.

## Rollback

- Tag latest to previous version

  ```bash
  docker tag "$image_name":"$image_previous_tag" "$image_name":latest
  ```

## Patch

patching depends on the method used for debugging. In case of running container you can just commit it. For exited container which was run using custom entry point, entry point is overwritten. So the patching required to revert the entry point.

### Docker was exec-ed

- Commit the live-debugging container.

  ```bash
  docker container commit "$container_name" "$image_name":"$image_tag"-patched
  ```

- Kill the live-debugging container

  ```bash
  docker container kill "$container_name"
  ```

- Tag the patched version to latest.

  ```bash
  docker tag "$image_name":"$image_tag"-patched "$image_name":latest
  ```

- Bring the latest service docker up.

### Docker was exec-ed (entry point has changed)

- Find the old entry point

  {% raw %}

  ```bash
  docker image inspect "$image_name":"$image_tag" --format "Entrypoint {{json .Config.Entrypoint}}"
  ```

  {% endraw %}

- Find the old cmd 

  {% raw %}

  ```bash
  docker image inspect "$image_name":"$image_tag" --format "CMD {{json .Config.Cmd}}"
  ```

  {% endraw %}

- Commit the docker with the old entry point and cmd

  ```bash
  docker container commit -change="$old_entrypoint" --change="$old_cmd" "$container_name" "$image_name":"$image_tag"-patched
  ```

- Kill the live-debugging container

  ```bash
  docker container kill "$container_name"
  ```

- Tag the patched version to latest.

  ```bash
  docker tag "$image_name":"$image_tag"-patched "$image_name":latest
  ```

- Bring the latest service docker up.

# Cleaning up

- Delete exited container.

  {% raw %}

  ```bash
  docker ps -a -f "status=exited" --format "{{json .Names}}" | xargs -r docker rm
  ```

  {% endraw %}

- Delete untagged images.

  ```bash
  docker images prune
  ```

# Resources

- [`docker ps`](https://docs.docker.com/engine/reference/commandline/ps/)
- [`docker images`](https://docs.docker.com/engine/reference/commandline/images/)
- [`docker image inspect`](https://docs.docker.com/engine/reference/commandline/image_inspect/)
- [`docker container inspect`](https://docs.docker.com/engine/reference/commandline/container_inspect/)
- [`docker logs`](https://docs.docker.com/engine/reference/commandline/logs/)
- [`docker container exec`](https://docs.docker.com/engine/reference/commandline/container_exec/)
- [`docker run`](https://docs.docker.com/engine/reference/commandline/run/)
- [`docker container commit`](https://docs.docker.com/engine/reference/commandline/container_commit/)
- [`docker image prune`](https://docs.docker.com/engine/reference/commandline/image_prune/)
- [`--format`](https://docs.docker.com/config/formatting/)
