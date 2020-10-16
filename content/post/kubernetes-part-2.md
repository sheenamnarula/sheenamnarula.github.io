+++
title = "Kubernetes Local System Set up"
featured = true
publishDate = 2020-10-16
subtitle = "Get started with Kubernetes on local system"


# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

# Get started with Kubernetes on local system 

To get started with kubernetes on your local system, you can use minikube. Minikube is basically local kubernets which helps to learn and develop kubernetes locally.All you need is Docker (or similarly compatible) container or a Virtual Machine environment

Installation process and important commands of minikube is given as below :

## Installation of minikube on Linux  
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-
 ```
 ```
 sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

## Command to Start cluster 
```
minikube start
```

## Command to Stop cluster
```
minikube stop

```
## Command to Delete cluster
```
minikube delete --all

```

## Minikube Dashboard  
There are commands to manage and access cluster but for ease, we will use dashboard provided by minikube where each and every detail of cluster can be seen and managed.
To launch minikube dashboard, run the following command in terminal : 

```
minikube dashboard
```
 
## Install kubectl (Command line interface) 
The Kubernetes command-line tool, kubectl, allows you to run commands against Kubernetes clusters. You can use kubectl to deploy applications, inspect and manage cluster resources, and view logs. 

```
sudo snap install kubectl --classic
```

## Commands to create kubernetes objects(after describing yaml files):

```
kubectl apply -f ${fileName}.yaml
kubectl create -f ${fileName}.yaml
```

### This was very basic understanding of minikube i.e local kubernetes. In the next part, we will look into the kubernetes configuration file. For this, we will deploy a Node application for better understanding of concepts.