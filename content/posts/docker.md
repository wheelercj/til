+++
title = 'Docker'
date = 2024-01-24T13:10:44-08:00
lastmod = 2024-02-22T18:48:05-08:00
+++

[Docker](https://www.docker.com/) is a tool that makes running software easier by creating a _container_, which is like a little virtual computer with a more predictable configuration than most computers. Containers are very portable, by which I mean they can be created in and run in any operating system that can run Docker. For example, a container could run Linux within it, and the container itself could run on Mac, Windows, and Linux. They're not the same as virtual machines though; containers are more lightweight and easier to automate.

Using Docker can significantly simplify the setup and deployment for software. The highlighted parts of the image below show the setup instructions for [a Discord bot I made](https://github.com/wheelercj/parhelion) before and after configuring it to run in Docker.

![before-and-after-dockerization.png](/before-and-after-dockerization.png)

The old way took a few hours every time I had to set up the bot. The new way takes only a few minutes after the first setup.

If you're familiar with virtual environments, such as the ones commonly used by the Python community, think of Docker like a big virtual environment that works for any programming language.

## how to get started with Docker

There are already many guides and tutorials I'll let you find. For me, it was helpful to watch multiple videos about the basics of what Docker does.

## Docker commands

* [`docker` official documentation](https://docs.docker.com/engine/reference/commandline/cli/)
* [`docker compose` official documentation](https://docs.docker.com/compose/reference/)
* The `docker-compose` tool has been deprecated in favor of the newer `docker compose` command.

Docker tends to be easier to use when you have a docker-compose.yml file and use the `docker compose` command to create and manage containers and their volumes.

* `docker compose up -d` follows instructions in docker-compose.yml to build and run the app. Images may be built and/or downloaded from [Docker Hub](https://hub.docker.com) if needed before containers are created from the images. The `-d` makes the containers run in detached mode, i.e. they run in the background.
* `docker compose logs -ft` to see the live Docker logs. Note that some apps have logs of their own that may be accessible somewhere else.
* `docker compose up -d --build` to rebuild images and to create and run the containers.
* `docker compose up -d --pull=always` to redownload images from Docker Hub and to create and run the containers.
* `docker compose ps` to list all containers that have not been stopped and see their statuses.
* `docker ps -a` to list all containers and see their statuses.
* `docker image ls` or `docker images` to list all images.
* `docker volume ls` to list all volumes.
* `docker compose exec containerName /bin/bash` to start an interactive Bash TTY inside a running container.
* `docker compose exec containerName sh` to start an interactive shell TTY inside a running container.
* `docker compose pause` to pause the containers.
* `docker compose unpause` to unpause paused containers.
* `docker compose stop` to stop the containers (this clears their memory).
* `docker compose start` to start stopped containers.
* `docker compose down` to stop and delete the containers. Volumes persist.
* `docker compose rm` to delete stopped containers. Volumes persist.
* `docker volume rm volumeName` to delete a volume.
* `docker image rm imageName` to delete an image.
* `docker container prune` to delete containers that failed.
* `docker image prune` to delete unused images.
* `docker build -t imageName .` to build a new image in the current directory.
* `docker run -it imageName` to create and run a container interactively.
* `docker run -pd 12345:4000 --restart unless-stopped --name containerName imageName` to create and run a new container from an image, exposing port `12345` with internal app port `4000`.

## pushing images to Docker Hub

1. Make sure the Docker engine is running, such as by opening Docker Desktop.
2. `docker login -u userName` and then enter an access token in place of a password.
3. `docker compose build`
4. `docker tag appName userName/appName`
5. `docker push userName/appName`
6. `docker tag userName/appName userName/appName:versionString`
7. `docker push userName/appName:versionString`

`docker tag` and `docker push` are used twice because not specifying a tag uses the default tag value `latest`.

More details can be found in [Publish your image](https://docs.docker.com/guides/walkthroughs/publish-your-image/) by Docker.

## security

Containers, and even virtual machines for that matter, are not necessarily secure enough to safely run arbitrary code within. Sandbox escapes are possible. Online code-running services like [tio.run](https://tio.run/#) appear to usually use [Security-Enhanced Linux (SELinux)](https://en.wikipedia.org/wiki/Security-Enhanced_Linux).

When running Docker on a Linux machine that is using UFW (Uncomplicated Firewall), Docker may bypass the firewall and create a security vulnerability. See [How to fix the Docker and UFW security flaw (2018)](https://www.techrepublic.com/article/how-to-fix-the-docker-and-ufw-security-flaw/) for details. Although that page _might_ be outdated, apparently [Podman is generally more secure than Docker](https://betterstack.com/community/guides/scaling-docker/podman-vs-docker/).
