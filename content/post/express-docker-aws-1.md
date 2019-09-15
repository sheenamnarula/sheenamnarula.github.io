+++
title = "Node-Docker-Aws Part-1"
featured = true
publishDate = 2019-06-28
subtitle = "This article is about dockerising a node app."


# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

First of all, make a project in node-express-mongo and dockerise it. Here I am giving a github link of a basic node-express app made along with graphql as this has become my favourite language because of its advantage of providing independence to front-end developers.

#### Github link for dockerised app : https://github.com/sheenamnarula/node-graphql-docker-aws

# Docker File

Lets understand first, what is the meaning of lines written in the docker file.

```
From node:8.9.0
```

This line specifies the base image.Every docker file starts with a FROM instruction. As we are writing here for node app, so we need to set a node environmnent for the app. Here node:<version> is the base image along with the required version for our app ie. 8.9.0

```
WORKDIR /app
```

This line refers to a directory in which we are going to keep our application files.Basically WORKDIR sets a directory where another commands like COPY, RUN, CMD, ADD can be run. In short, it is providing an entry point of app directory.

```
COPY package\*.json ./
```

To start a project or run a project, we need to install node modules and as we know in a node app, package.json is a file where dependencies of project is documented. So we are copying package.json in working directory so that further instructions can install node modules using this file. Here package\* refers to package.json and package.lock.json files.

```
RUN npm install
RUN npm install nodemon babel-cli babel-preset-env
```

These both lines contain RUN command. After copying package.json in work directory that is suppose to be entry point of our source files,using RUN command we are installing node modules and required dependencies for our project. Basically RUN command is used for the command that we run in a terminal and then it commits a new image which is further used by next instructions of docker file

```
EXPOSE 3007
```

This line is very important to understand as it defines which port of container is exposed.When we give any port with this command, that means that port of container is exposed.Means if we want to access app, we have to write the hostname simply i.e we need to write port 80 on browser. But if we write publish port in docker run command with expose port that means the app will be accesed through published port. In short, EXPOSE is used to open port for network but publish is used to map the opened port to public accessible port.

```
COPY . /app
```

Here we are copying the all content of app to our container working directory so that app can be run.

```
CMD npm run start
```

This line refers to executing the command that is required to start the project.

### Difference between RUN and CMD -

Here is an important difference between RUN and CMD :

#### RUN -

Basically RUN command triggers when we are building docker image. After RUN command, image is committed and next command uses that committed image.

#### CMD -

Basically CMD command triggers when we launch the created docker image.Dockerfile can have only one CMD command and it can be overriden while starting a container i.e. executing docker run $image $other_command

This is all about a docker file. Environment variables can also be included using ENV command.
Now this is all about one container which will contain app. But here database required is mongo db and we also need a container for mongo db.

NOTE : It is possible to run mongo db and app in one container but it will create problem in scaling because if we need to scale app, thereby we will be scaling mongo db as well and moreover, it is difficult to maintain same data availability for all container apps in this case. So we will have one container for mongo db service following microservice architecture i.e. every service is running independently.

To manage more than one container we will go for a tool named Compose. Compose is a tool that is used to define and run multi-container docker applications.In this, a YAML file is used to configure multiple containers of application services.Then with a single command, we can create and start all the services using yaml configuration file.

Here is the code for docker compose file and explanation of each line of code :

# Explanation of Docker Compose file :

```
version: "3" -
```

This line refers to the docker compose file format version.

```
services:
```

This line refers to the start of container configurations.A service definition contains configuration that is applied to each container started for that service.

```
app:
```

This line refers to the name of your service.

```
container_name: docker-node-mongo
```

By default, a random name is generated. To generate a meaningful name, we use container_name parameter in config.

```
restart: always
```

By default behaviour of container is that it never restarts. By setting restart to always, we are making container to opt restarting behaviour.

```
build: .
```

This option is used when we have to make an image from a docker file. Relative path is given in this option so that docker can look for Dockerfile according to given path to build image.\

```
ports:
  - "80:3007"
```

This option is used to mention the exposed port of container. HOST:CONTAINER is short syntax to metion ports.

The long form syntax allows the configuration of additional fields that can’t be expressed in the short form.

target: the port inside the container
published: the publicly exposed port
protocol: the port protocol (tcp or udp)
mode: host for publishing a host port on each node, or ingress for a swarm mode port to be load balanced.

```
ports:
  -target: 80
  published: 8080
  protocol: tcp
  mode: host
```

```
depends_on:
  - mongo
```

This line express the dependencies of one container to other. To start a container,the containers on which it is dependent, will be started first

```
mongo:
  container_name: mongo
  image: mongo
```

This will check the mongo image if it is available locally and in case of unavailability, image will be downloaded from docker hub(github for docker images).

```
ports:
 - "27017:27017"
```

Here is on more command like depends_on i.e. links. But link is deprecated now. depends_on gives us start order but links just to link one container to another.But now, if containers are placed in same network, they can connect with each other by using their name.

Now by running a single command, "docker-compose up", we can see two containers running one is our app container and other is mongo container.

Note: In project here is one commented line , `mongodb://mongo:27017/expGraphqlDemo`. In this mongo is container name and 27017 is container's published port.But for deployment purpose, we are making it configurable and will pass as environment variable while deployment.
