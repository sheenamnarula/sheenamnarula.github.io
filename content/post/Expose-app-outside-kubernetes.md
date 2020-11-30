+++
title = "Expose Application from outside of Cluster"
featured = true
publishDate = 2020-10-26
subtitle = ""

# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

There are different ways to expose application to outside world which have been explained as under :

### hostNetwork : true

Applies to : Pods
When a pod is configured to ``` hostNetwork : true  ``` , the applications running in such a pod can directly see the network interfaces of host machine.
Here is an example of this method :

```
apiVersion: v1
kind: Pod
metadata:
  name: influxdb
spec:
  containers:
    - name: influxdb
      image: influxdb
```
Now after running this pod on cluster, you can verify that this influxdb is running with :

```
curl -v http://hostIp:8086/ping
```
The above command will respond back with status 204 No Content while working properly.

#### When not to use : 
Note that every time the pod is restarted Kubernetes can reschedule the pod onto a different node and so the application will change its IP address. Besides that two applications requiring the same port cannot run on the same node. This can lead to port conflicts when the number of applications running on the cluster grows.

#### When to use :
When a direct access of host networking is required.

### hostport

Applies : Containers 

The container port will be exposed to the external network at
hostIp:hostPort where hostIp is Ip of node where pod is hosted and hostPort is the port requested by user.

```
apiVersion: v1
kind: Pod
metadata:
  name: influxdb
spec:
  containers:
    - name: influxdb
      image: influxdb
      ports:
        - containerPort: 8086
          hostPort: 8086
```

#### Drawbacks : 
Using the hostPort to expose an application to the outside of the Kubernetes cluster has the same drawbacks as the hostNetwork approach discussed in the previous section. The host IP can change when the container is restarted, two containers using the same hostPort cannot be scheduled on the same node 

### NodePort

Applies to : Service 

By default Kubernetes services are accessible at the ClusterIP which is an internal IP address reachable from inside of the Kubernetes cluster only. The ClusterIP enables the applications running within the pods to access the service. To make the service accessible from outside of the cluster a user can create a service of type NodePort. At first, let’s review the definition of the pod that we’ll expose using a NodePort service:

```
apiVersion: v1
kind: Pod
metadata:
  name: influxdb
  labels:
    name: influxdb
spec:
  containers:
    - name: influxdb
      image: influxdb
      ports:
        - containerPort: 8086
```

When creating a NodePort service, the user can specify a port from the range 30000-32767, and each Kubernetes node will proxy that port to the pods selected by the service. A sample definition of a NodePort service looks as follows:

```
kind: Service
apiVersion: v1
metadata:
  name: influxdb
spec:
  type: NodePort
  ports:
    - port: 8086
      nodePort: 30000
  selector:
    name: influxdb

```

After the service has been created,  the kube-proxy component that runs on each node of the Kubernetes cluster and listens on all network interfaces is instructed to accept connections on port 30000. The incoming traffic is forwarded by the kube-proxy to the selected pods in a round-robin fashion. You should be able to access the InfluxDB application from outside of the cluster using the command:

```
curl -v http://hostIp:30000/ping
```
The NodePort service represents a static endpoint through which the selected pods can be reached.

### LoadBalancer : 
The LoadBalancer service applies to kubernetes service.
