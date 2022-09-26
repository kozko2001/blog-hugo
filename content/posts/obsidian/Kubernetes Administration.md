
---
title: Kubernetes administration
date: 2022-09-25 00:00:00
---
---

# Kubernetes administration

## Components of the cluster
### ETCD 
> a key-base database that is high available. Used to store the current state of the cluster

### kube-apiserver
> Central api that all components use to ask for change or query info. Also is the API that we use with kubectl
### Scheduler
> In charge to decide to wich node each pod has to go
### Kube Controller Manager
> Manager of diferent logics in the k8s cluster

### Kubelet
> is the captian in each worker nodes

### kube-proxy
> A components does action to allow different worked nodes talk to each other




## Components of an application

### POD
- minimum components
- it can have 1 or more container

### Replicaset
- ensures that n  amount of containers are up at all time

### Deployment
- allow to change pod from one version to another
	- rollout etc...
- the yaml definition is quite similar to the `replicaset`

### Services
> enable connectivity between pods

- Types:
	- **Node port** -> opens a port on the worked node, and maps this port to the pod
	- **cluster ip** -> creates a (virtual ?) ip in the cluster, grouping the pods in the same service. You use the service to communicate
	- **load balancer** -> to use a cloud LB