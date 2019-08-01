+++
title = "Kubernetes Part-1"
featured = true
publishDate = 2019-07-29
subtitle = "This article is about Kubernetes architecture."


# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

## Kubernetes Vocab : 

### Node :

It is an instance of computer which is also known as worker nodes.

### Pods :

It is a smallest unit of kubernetes that we can deploy on kubernets cluster.It contain container's image.
Bascially a pod is a collection of more than one conatiners which are supposed run on one host logically.

When a pod is created, an ip address is assigned to it.When a worker node dies, replica of that pod is created but with different ip address and different volumes. That means everything related to pod lifecycle dies with that pod.(stable ip address concept)

### Services :

Services are the end points that export ports to outside world and map the ports to pods.

### Deployment :

It represents a set of multiple identical pods.Deployments run multiple instances or replicas of your application.It ensures the availability of one or more instances of app to serve user requests.Deployments are managed by kubernetes deployment controller.
Deployments use a Pod template, which contains a specification for its Pods. The Pod specification determines how each Pod should look like: what applications should run inside its containers, which volumes the Pods should mount, its labels, and more.

When a Deployment's Pod template is changed, new Pods are automatically created one at a time.


# KUBERNETES ARCHITECTURE :
![Example image](/img/kubernetes-architecture.png)


### Kubernetes Master Components: Etcd, API Server, Controller Manager, and Scheduler :

Kubernetes master is considered as the brain of kubernetes cluster. It run Etcd, Scheduler, Controller Manager and Api Server inside it.Lets discuss there components briefly so that working on kubernetes should not appear to be strange and knowing components of kubernetes master will help us in a significant way in creating a working image of kubernetes master.

#### Etcd :

Etcd is a very important part of kubernetes master node. It saves the configuration data of kubernetes cluster like which nodes are there,how many pods are there and which pod is running on which node and a lot more information regarding cluster state. Kubernetes master reads and write data to etcd to get the current state and decides the required logical operations to be performed to achieve the desired state.
Etcdctl is a command line interface to manage Etcd through which many operations for etcd can be performed like adding and removing key-value pairs(etcd data storage format is key value pair), verify cluster health, generating database snapshots(As Kubernetes master is highly dependent on etcd for data, so we should have a backup plan for etcd. We can save a snapshot of etcd by using etcdctl save snapshot command).

Etcd also impelements a "watcher" feature in which for every key there is a watcher. Whenever key changes, watcher is notified and in return an event is triggered for Api server. After listening to event, api server takes important decisions of operations to be performed to move current state towards desired state.

#### Api Server : 
(The REST API is the fundamental fabric of Kubernetes. All operations and communications between components, and external user commands are REST API calls that the API Server handles. Consequently, everything in the Kubernetes platform is treated as an API object and has a corresponding entry in the API.)
Kubernetes api server is a main management point of kubernetes cluster.Basically when we interact with kubernetes using kubectl command line interface, we are actually communicating with Api server component. Only Api server component directly communicates with Etcd to read, write and update objects after validating requests. Rest all components has to go through Api server to work with cluster state.
The API Server also implements a watch mechanism (similar to etcd) for clients to watch for changes. This allows components such as the Scheduler and Controller Manager to interact with the API Server in a loosely coupled manner.
For example : 

![Example image](/img/createPod.png)

1. kubectl writes to api server
2. Api server writes to etcd after validating request.
3. etcd notifies back to api server.
4. Api server invokes scheduler.
5. Scheduler decides where to run the pod on and return back to Api server.
6. Api persists data in etcd.
7. Etcd writes back to api server.
8. Api server invokes the Kubelet in corresponding node.
9. Kubelet talks to docker daemon using the api over docker socket to create continer.
10. Kubelet updates the status to Api server.
11. Api server interacts with etcd to persist new state.

#### Controller Manager : 
Controller manager watches the cluster state through Api server and when it gets notified, it makes necessary changes to move current state of cluster towards desired state.For e.g. Replication controller always maintains the required number of replicas of pods.

#### Scheduler : 
Scheduler watches for unscheduled pods and decides as which pod has to run on which node.
Once a pod's binding to node is done, regular task of Kubelet is invoked which in turn calls container engine like docker to create and start container.

### Kubernetes Node Components : 

Basically, Kubernetes node runs Kubelet and Service Proxy components. It also runs container engine like Docker which in turn runs containerized applications.

#### Kubelet : 
It's an agent that runs on each node and being a watcher it reports activities of pods to api server.It makes sure that pods attached to its node are running. It talks to docker daemon through docker socket api and which in turn is responsible for running containers.

Jobs of kubelet : 
1. Run the pods.
2. Report the status of node and pods to api server.
3. Run container probes.

###### cAdvisor
The Kubelet ships with built-in support for cAdvisor, which collects, aggregates, processes and exports metrics (such as CPU, memory, file and network usage) about running containers on a given node. cAdvisor includes a built-in web interface available on port 4194 (just open your browser and navigate to http://<node-ip>:4194/).

You can view the cAdvisor /metrics endpoint by issuing a GET request to http://<node-ip>:4194/metrics.

#### Service Proxy : 
Service Proxy runs on each node and is responsible for watching the api server for pods and services definitions' changes to keep the entire network's configuration up to date,ensuring that one pod can talk to another pod,one node can talk to another node, one container can talk to another container.In addition to this, it maintains all ip route tables so that it can redirect user request to a correct backend resource. That is why, when we hit the Node port, even if app is not available on that node but it redirects the request to the correct backend resource for execution. 