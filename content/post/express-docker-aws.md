+++
title = "Node-Docker-Aws Part-2"
subtitle = "This article is about deploying two containers(api + database) using AWS Elastic Container Service"


# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

First of all, make a project in node-express-mongo and dockerise it. Here I am giving Dockerfile for a very basic node app.

#github link for dockerised app :

I am taking as an amazon account is already set up to use the Amazon Elastic Container Service(ECS).

Steps to deploy app -

1. Dockerise app (link for previous article)
2. We need to keep image of app somewhere from where it is pulled while starting container.We can do two things here. Either we can use Docker Hub or we can use Amazon Elastic Container Registry(ECR) service. In this tutorial, i am using ECR to keep created images.

So basically step starts from here, get a repository url by creating a repository
