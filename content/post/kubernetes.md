+++
title = "KUBERNETES"
subtitle = "This article is about running containers on kubernetes cluster."


# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

## Kubernetes Vocab

### Node :

It is an instance of computer which is also known as worker nodes.

### Pods :

It is a smallest unit of kubernetes that we can deploy on kubernets cluster.It contain container's image.
Bascially a pod is a collection of more than one conatiners which are supposed run on one host logically.

When a pod is created, an ip address is assigned to it.When a worker node dies, replica of that pod is created but different ip address and different volumes. That means everything related to pod lifecycle dies with that pod.(stable ip address concept)

### Services : 
Services are the end points that export ports to outside world and map the  ports to pods.

### Deployment :

### Installation of kubernetes : 

Let us install Minikube to run single-node kubernetes  cluster in a virtual machine on your personal computer to work locally and kubectl as command line interface of kubernetes.

Let us check first whether virtualization is supported on Linux. For this,run the following command and verify that the output is non-empty:
egrep --color 'vmx|svm' /proc/cpuinfo

## Install kubectl : Link for installation

https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-on-linux

#### For ubuntu, here are the commands to install kubectl :

      sudo apt-get update && sudo apt-get install -y apt-transport-https
      curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
      echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
      sudo apt-get update
      sudo apt-get install -y kubectl

##  Install Minikube : 
### Link for Installation : https://kubernetes.io/docs/tasks/tools/install-minikube/

# Architecture explanation of kubernetes : 

### Kubernetes Master Components: Etcd, API Server, Controller Manager, and Scheduler : 
Kubernetes master is considered as the brain of kubernetes cluster. It run Etcd, Scheduler, Controller Manager and Api Server inside it.Lets discuss there components briefly so that working on kubernetes should not appear to be strange and knowing components of kubernetes master will help us in a significant way in creating a working image of kubernetes master. 
#### Etcd : 
Etcd is a very important part of kubernetes master node. It saves the configuration data of kubernetes cluster like which nodes are there,how many pods are there and which pod is running on which node and a lot more information regarding cluster state. Kubernetes master reads and write data to etcd to get the current state and decides the required logical operations to be performed to achieve the desired state.
Etcdctl is a command line interface to manage Etcd through which many operations for etcd can be performed like adding and removing key-value pairs(etcd data storage format is key value pair), verify cluster health, generating database snapshots(As Kubernetes master is highly dependent on etcd for data, so we should have a backup plan for etcd. We can save a snapshot of etcd by using etcdctl save snapshot command).

Etcd also impelements a "watcher" feature in which for every key there is a watcher. Whenever key changes, watcher is notified and in return an event is triggered for Api server. After listening to event, api server takes important decisions of operations  to be performed to move current state towards desired state.

#### Api Server : 


