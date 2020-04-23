# Kubernetes Cheat Sheet for GKE
This is my cheat sheet for interacting with Kubernetes clusters in Google Cloud Kubernetes Engine. Kindly note that I am no expert and there might be some errors in some commands. If you do find one, please let me know so that I can fix it. This is in conjunction with my Google Cloud Associate Cloud Engineer training. Cheers!

## K8 101. A brief introduction of the resources in Kubernetes
### Containers
Containers are a package of application and its dependencies. It has a less overhead than virtual machines, but it must be run on the same operating system. You cannot directly run a Linux-based container to Windows OS, vice-versa. Containers provide complete isolation of your application and you can configure the amount of CPU and memory for each container. 
See [Containers by Google](https://cloud.google.com/containers)

### Pods
Pods are the smallest deployable unit in Kubernetes. Pods can contain single or multiple containers (but not usually the same kind). They are mortals (can die anytime heh).

### Nodes
A node is a virtual machine or a physical computer. This is where your pod runs. There are types of nodes (this is how I define it), the worker nodes and the master. A worker node is where your pods are running. A master is a node that watches worker nodes in the cluster and is responsible for the actual orchestration.

### Cluster
A cluster is a group of nodes (connected by a network)

## K8 Components
1. API Server
    - the frontend for Kubernetes
2. etcd
    - a keystore
    - a distributed key-value store used by K8 to store data used to manage the cluster
3. Scheduler
    - responsible for distributing work to containers/pods on nodes
    - looks for new containers and assigns them to nodes
4. Controller
    - the brain behind the orchestration
    - they are responsible for noticing & responding when nodes or containers/endpoints goes down
5. Container Runtime
    - underlying software to run containers (docker)
6. kubelet
    - an agent that runs on each node in the cluster

## gcloud and kubectl. Which is which?
Yeah. If you're new with Google Kubernetes Engine, you might get confused between `gcloud` and `kubectl`. We use `gcloud` for creating, updating, or deleting a cluster. We also use it for building container image. Use `gcloud` to manage Google Cloud Resources.

Now for interacting with our cluster, we use `kubectl`. Use `kubectl` for deploying/updating/deleting resources inside Kubernetes. 