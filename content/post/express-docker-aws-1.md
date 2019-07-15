+++
title = "Node-Docker-Aws Part-1"
subtitle = "This article is about dockerising a node app."


# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

First of all, make a project in node-express-mongo and dockerise it. Here I am giving a github link of a basic node-express app made along with graphql as this has become favourite language because of its advantage of providing independence to frontend people.

#github link for dockerised app :

# Docker File

Lets understand first, what is the meaning of lines written in the docker file.

# From node:8.9.0 -

    This line specifies the base image.Every docker file starts with a FROM instruction. As we are writing here for node app, so we need to set a node environmnent for the app. Here node:<version> is the base image along with the required version for our app ie. 8.9.0

# WORKDIR /app -

    This line refers to a directory in which we are going to keep our application files.Basically WORKDIR sets a directory where another commands like COPY, RUN, CMD, ADD can be run. In short, it is providing an entry point of app directory.

COPY package\*.json ./

# RUN npm install

# RUN npm install nodemon babel-cli babel-preset-env

    These both lines contain RUN command. After copying package.json in work directory that is suppose to be entry point of our source files,using RUN command we are installing node modules and required dependencies for our project. Basically RUN command is used for the command that we run in a terminal and then it commits a new  image which is further used by  next instructions of docker file

EXPOSE 3007

COPY . /app

CMD npm run start
