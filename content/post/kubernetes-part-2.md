+++
title = "Kubernetes Part-2"
subtitle = "This article is about installation and deployment file of Kubernetes."


# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

Let us install Minikube to run single-node kubernetes cluster in a virtual machine on your personal computer to work locally and kubectl as command line interface of kubernetes.

Let us check first whether virtualization is supported on Linux. For this,run the following command and verify that the output is non-empty:
egrep --color 'vmx|svm' /proc/cpuinfo

## Installation link for kubectl

https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-on-linux

## Installation link for Minikube :
 https://kubernetes.io/docs/tasks/tools/install-minikube/

Here I am explaining deployment file of a very simple node-express-mongo application.

 

