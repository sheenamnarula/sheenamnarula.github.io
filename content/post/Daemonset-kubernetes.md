+++
title = "Daemonset in Kubernetes"
featured = true
publishDate = 2020-10-27
subtitle = ""

# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

### What is Daemonset ?

Replica set ensures that number of pods mentioned in the config should be running.It does not care about as all pods are running in one node or different nodes.

Daemonset in kubernetes is a resource type which ensures the pod mentioned in config should run in every node.
Important points related to Daemonset :

- As nodes are added to the cluster,pods are added to them.
- As nodes are removed from the cluster, those Pods are garbage collected. 
- Deleting a Daemonset will clean up its pods created.

### Logging using EFK (Elasticsearch Fluentds Kubernetes) :





