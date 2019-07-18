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

#github link for dockerised app : https://github.com/sheenamnarula/node-graphql-docker-aws

I am assuming that an amazon account is already set up to use the Amazon Elastic Container Service(ECS).

Steps to deploy two containers(app + database) -

1. Dockerise app (link for previous article)
2. Create Registry(ECR)
3. Upload app image to ECR
4. Create task definition with two containers
5. Create a cluster
6. Create a service and run it.

## Practical Explanation of steps :

### 1. Dockerise app

        for this you can check this article : https://github.com/sheenamnarula/node-graphql-docker-aws (linkk for previous article)

### 2. Create Registry(ECR)

We need to keep image of app somewhere from where it is pulled while starting container.We can do two things here. Either we can use Docker Hub or we can use AWS Elastic Container Registry(ECR) service. In this tutorial,i am using ECR to keep the created images.

Log in to web console into your prefered region and choose ECR from services.

![Example image](/img/aws-images/choose-ECR.png)

There create a repository to store image of your app.After creating repository, you will see a button "View Push Commands" on right side.
![Example image](/img/aws-images/button-view-commands.png)

On clicking that button, you will get some commands that will be used to push image of app to this repository.
![Example image](/img/aws-images/push-commands.png)

### 3 . Upload image to ECR

Run the commands, to push the image to ECR.

#### Command 1.

        aws ecr get-login --no-include-email --region ap-south-1

This will help you to login to aws through cli.(Note : Install aws-cli to run these commands.)
( Link to install aws cli : https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html )

![Example image](/img/aws-images/aws-login.png)

#### Command 2.

      docker build -t node-express .

This command will help you in building image of your app. Run this command in the folder containing the app. -t is to give the name to your image. You can also customize it according to your preference so that you can find the created image easily.
![Example image](/img/aws-images/aws-login.png)

#### Command 3.

         docker tag node-express:latest 597357263415.dkr.ecr.ap-south-1.amazonaws.com/node-express:latest

This command is used to tag your created image to the ECR.
![Example image](/img/aws-images/build-image.png)

#### Command 4 .

         docker push 597357263415.dkr.ecr.ap-south-1.amazonaws.com/node-express:latest

This command is used to push the created image to ECR. This command can take few minutes to execute.
![Example image](/img/aws-images/pushing-image.png)

### 3. Create Task definitions

As we run docker commands like docker run in docker cli, here task definitions are used for this purpose. Every task consists of - docker containers details, port mappings, network details, environment variables, volumes if any, and the most important thing, image of app.
Choose Task Definitions in left navigation pane.

![Example image](/img/aws-images/task-definition.png)

Here we will define two containers in one task as running app willl contain api container and database container.

#### First Container : Api Container

Copy the url of your image that we pushed in ECR in second step.

![Example image](/img/aws-images/image-url.png)

Click on Create New Task Definition and choose EC2 and then click on next.
![Example image](/img/aws-images/ec2-selection-task-def.png)

Here you will get a form to define your task.
![Example image](/img/aws-images/form-1-task-def.png)

Fill out the required fields and click on Add Containers.
![Example image](/img/aws-images/add-container-button.png)

In add container form, specify the container name and memory required.
Then give the port mappings i.e host port and container port.
![Example image](/img/aws-images/container-1-port.png)

Give Environment variables using Key-value pair(In this project, we are using mongo db as environment variable)
![Example image](/img/aws-images/env-variables.png)

In network links, you can declare the linking of other containers with this container simply by following syntax - othercontainer: alias
![Example image](/img/aws-images/link.png)

Here we are running database in second container and we are gonna name it as mongo-container(yet to be defined)
We are linking this container to database container.
Then click on create and you will get your api container created.

#### Second Container : Database Container

For this container, we need a mongo image and this can be directly pulled from Docker Hub. Here is the required url for mongo image : registry.hub.docker.com/library/mongo:latest

Now we need to be careful while naming second container as we have mentioned in the linking of first container as "mongo-container". So for correct linking, we need to keep the name of our db container as "mongo-container"

![Example image](/img/aws-images/container-2.png)

and also mention the hostname as mongo-container.

![Example image](/img/aws-images/hostname.png)

Now click on create option and you will get your task definition created with two containers.

![Example image](/img/aws-images/added-containers.png)

### 4. Create Cluster :

Cluster is where container runs.

Choose Clusters from left navigation pane and choose create cluster.Creating cluster is like setting up an EC2 instance.After clicking on create cluster, choose EC2+Linux and create cluster with options vpc - create new vpc group,instance type- m4.large and number of required instances.
![Example image](/img/aws-images/create-cluster-button.png)

![Example image](/img/aws-images/selecting-ec2-linux-cluster.png)

Configuration of cluster :
![Example image](/img/aws-images/configure-cluster.png)

![Example image](/img/aws-images/configure-cluster-2.png)

Now you can see the created cluster, on clicking that cluster, you can see tabs for task definition, ec2 instance and services.

![Example image](/img/aws-images/created-cluster.png)

### 5. Create Service :

Service is used to run your defined tasks in cluster.
Click on create service and fill the required fields.

![Example image](/img/aws-images/configure-service.png)

![Example image](/img/aws-images/configure-service-2.png)

Creating service :
![Example image](/img/aws-images/creating-service.png)

![Example image](/img/aws-images/created-service.png)

Choose the task definition that have been created in step 3 and run the service.

Initially it will show pending state and soon it will be in running state.
![Example image](/img/aws-images/pending-status.png)

When it is in running state, you can go to cluster and then click on ec2 instance.
![Example image](/img/aws-images/running-status.png)

On clicking that, details of that instance will appear. From there copy the public dns.
![Example image](/img/aws-images/ec2-public-dns-url.png)

Paste the copied address in browser and you can see your app in running state.
![Example image](/img/aws-images/working-example.png)
