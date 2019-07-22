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

### Deployment :

Let us install Minikube to run single-node kubernetes to work locally.
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
