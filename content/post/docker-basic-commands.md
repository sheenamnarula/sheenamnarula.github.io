+++
title = "Basic Docker Commands"
subtitle = "This article lists all basic commands of docker."


# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

### Show commands and Management commands

      $ docker

### Docker version :

      $ docker --version

### Show info like number of containers

      $ docker info

## Commands required for Containers

#### Command to run a container in foreground :

      $ docker container run -it -p 80:80 {image name}

Example : docker container run -it -p 80:80 nginx

#### Command to run a container in backround :

      $ docker container run -d -p 80:80 {image name}

#### Short hand command

      $ docker container run -d -p 80:80 {image name}

#### Naming custom names to container

      $ docker container run -p 80:80 --name {container name} {image name}

Example : docker container run -d -p 80:80 --name nginx-server nginx

### Purpose of "run" in command :

- It actually looks for image in local cache.
- If image is not found, it looks into Docker Hub where default image repo may exist(its like github for docker images).
- It pulls it down from there and stores into local image cache.
- Starts in a new container.
- As we know syntax for port specification is HOST:CONTAINER port. So here we can access on port 80.
- We can also access it on any port by changing host port. For e.g. , if we want access on port 3000, then we need to write here 3000:80.

#### Commands for listing containers

These two commands gives us running containers.

        $ docker ps
        $ docker container ls

This command will give us all containers(including those containers as well which are not running).

        $ docker container ls -a

#### Commands to stop container
