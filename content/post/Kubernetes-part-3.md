+++
title = "Kubernetes Configuration file"
featured = true
publishDate = 2020-10-16
subtitle = "Deployment of Node App to kubernetes"

# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

### In this post, we will understand the different parts of configuration file of kubernetes by deploying a node application.

For this post, you can find github code at : 
 ```
https://github.com/sheenamnarula/Node-mongo-kubernetes
 ```
Refer this repository that contains dockerised node application code  and configuration files for kubernetes deployment for better understanding.

### Second Option : 
Create a node app and dockerise it. For dockerisation of node app, you can follow below post :
```
 http://sheenamnarula93.com/post/express-docker-aws-1/

 ```

 ## Kubernetes Configuration File :

 Folder Location for files in cloned repository : k8s
```
 Node app file : k8s/node-app.yaml

 Mongo file : k8s/mongodb.yaml
```
 ## Explanation of files : 

 ```
 apiVersion : apps/v1
 ```
 - This line describes the Kubernetes API versions to be used to create the resource.

 ```
 kind : Deployment
 ```
 - This line describes the type of resource to be created.

 ```
 metadata : 
  labels : 
    app : node-app
  name : node-app

 ```
### Metadata : 
- attaches meta-information regarding the resource such as its name or labels.

```
spec:
  replicas : 1
  selector :
    matchLabels : 
      app : node-app-pod
  template : 
    metadata : 
      labels : 
        app : node-app-pod
    spec :
      containers : 
      - name: node-application
        env :
        - name : DB_URI
          value : mongodb://mongodb-service:27017/node-application
        image : sheenam1993/node-application
        ports : 
        - containerPort: 3007
      restartPolicy: Always

```
### Spec 
- describes the specifications of resources

 The deployment resources are used to manage and control the life cycle of applications Pods.
As a result,the spec section for the deployment resource is containing information about the applications Pod and how to control them, below is a brief description of the basic sections that are required for Deployment Spec:

- ### Replicas:
 an integer that specifies how many pods the deployment should create.

- ### Selectors:
 this configuration section specifies the conditions used to select the Pods managed by Deployment. For instance, in the example that we are going to use, Pods that have the label app: mongodb-pod will be managed by the Deployment resource.

### Template :
 this section contains the configurations of the Pods.

The Template section contains the following subsections:

- ### Metadata
The information that will be attached to every Pod created by our Deployment. The labels defined in this section must match the ones used in the selector sections so that the deployment can manage the Pods after their creation.

- ### Spec
The specifications of the Pod containers (notice that containers sections is a list and can include more than one container definition). Here we can define specific container configurations such as the image name, the attached volumes, restart policy and used ports.

## Service in Kubernetes

```
apiVersion: v1
kind: Service
metadata:
  labels:
    app: node-app-pod
  name: node-app-service
spec:
  ports:
  - port: 8080
    targetPort: 3007
    nodePort: 30007
  selector:
    app: node-app-pod
  type: NodePort

```
 A service makes pods available for interaction to other application pods in the cluster. 

 Explanation of Service Code : 

 ```
 kind: Service
 ```
 Kind describes the type of resource to be created. So while creating service, its value is "Service"

```
metadata:
  labels:
    app: node-app-pod
  name: node-app-service
```

Metadata describes the information about the service. Here we have given two thing under meta data : labels and name.

A service can be called by another service in cluster by name.


```
spec:
  ports:
  - port: 8080
    targetPort: 3007
    nodePort: 30007
  selector:
    app: node-app-pod
  type: NodePort
```
Spec describes specifications of servoice. Here is description of spec code :

- ### ports 
 ports contain 3 parts further :
port : exposed port of service (for other services)
- ### targetPort 
 exposed port of a pod (means on which our app is running)
- ### nodePort 
exposed port to access service from outside the cluster (means if we have to expose the service to end user to run, we have to use nodePort)

- ### selector 
 the conditions used to select Pods managed by the service resource.

- ### type :
 Kubernetes supports a couple of service types for managing internal and external traffic. Since MongoDB should not be accessed by any external entity, we will create a ClusterIP service that will expose the service on a cluster-internal IP (only accessible by Pods in the same cluster).But for Node app we have created NodePort service type which can be accessed from outside the cluster as well.

