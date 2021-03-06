# CLI Commands for GKE

### Creating clusters (gcloud)
<details>
 <summary>Creating a zonal cluster</summary>

```bash
gcloud container clusters create [YOUR CLUSTER] --zone [ZONE]
```
</details>

<details>
 <summary>Creating a multi-zonal cluster</summary>

```bash
gcloud container clusters create [YOUR CLUSTER] --zone [ZONE] --node-locations [ZONE1-A],[ZONE1-B]
```
</details>

<details>
 <summary>Creating a regional cluster</summary>

```bash
gcloud container clusters create [YOUR CLUSTER] --region [REGION]
gcloud container clusters create [YOUR CLUSTER] --region [REGION] --node-locations [ZONE1-A],[ZONE1-B]
```
</details>

<details>
 <summary>Creating a private cluster with no client access to the public endpoint</summary>

```bash
gcloud container clusters create [YOUR CLUSTER] \
    --create-subnetwork name=[SUBNET NAME] \
    --enable-master-authorized-networks \
    --enable-ip-alias \
    --enable-private-nodes \
    --enable-private-endpoint \
    --master-ipv4-cidr [CIDR RANGE] \
    --no-enable-basic-auth \
    --no-issue-client-certificate
```

Where:
- `--create-subnetwork` causes GKE to automatically create a subnet
- `--enable-master-authorized-networks` specifies that access to the public endpoint is restricted to IP address ranges that you authorize.
- `--enable-ip-alias` makes the cluster VPC-native.
- `--enable-private-nodes` indicates that the cluster's nodes do not have external IP addresses.
- `--enable-private-endpoint` indicates that the cluster is managed using the private IP address of the master API endpoint.
- `--master-ipv4-cidr` specifies an RFC 1918 range for the master. This setting is permanent for this cluster.
- `--no-enable-basic-auth` indicates to disable basic auth for the cluster.
- `--no-issue-client-certificate` disables issuing a client certificate.

Creating a private cluster must comply with [RFC 1918](https://tools.ietf.org/html/rfc1918) for best practices.
</details>

<details>
 <summary>Creating a private cluster with limited access to the public endpoint</summary>

```bash
gcloud container clusters create [YOUR CLUSTER] \
    --create-subnetwork name=[SUBNET NAME] \
    --enable-master-authorized-networks \
    --enable-ip-alias \
    --enable-private-nodes \
    --master-ipv4-cidr [CIDR RANGE] \
    --no-enable-basic-auth \
    --no-issue-client-certificate
```

Where:
- `--create-subnetwork` causes GKE to automatically create a subnet
- `--enable-master-authorized-networks` specifies that access to the public endpoint is restricted to IP address ranges that you authorize.
- `--enable-ip-alias` makes the cluster VPC-native.
- `--enable-private-nodes` indicates that the cluster's nodes do not have external IP addresses.
- `--master-ipv4-cidr` specifies an RFC 1918 range for the master. This setting is permanent for this cluster.
- `--no-enable-basic-auth` indicates to disable basic auth for the cluster.
- `--no-issue-client-certificate` disables issuing a client certificate.

Creating a private cluster must comply with [RFC 1918](https://tools.ietf.org/html/rfc1918) for best practices.
</details>

<details>
 <summary>Creating a private cluster with unrestricted access to the public endpoint</summary>

```bash
gcloud container clusters create [YOUR CLUSTER] \
    --create-subnetwork name=[SUBNET NAME] \
    --no-enable-master-authorized-networks \
    --enable-ip-alias \
    --enable-private-nodes \
    --master-ipv4-cidr [CIDR RANGE] \
    --no-enable-basic-auth \
    --no-issue-client-certificate
```

Where:
- `--create-subnetwork` causes GKE to automatically create a subnet
- `--no-enable-master-authorized-networks` disables authorized networks for the cluster.
- `--enable-ip-alias` makes the cluster VPC-native.
- `--enable-private-nodes` indicates that the cluster's nodes do not have external IP addresses.
- `--master-ipv4-cidr` specifies an RFC 1918 range for the master. This setting is permanent for this cluster.
- `--no-enable-basic-auth` indicates to disable basic auth for the cluster.
- `--no-issue-client-certificate` disables issuing a client certificate.

Creating a private cluster must comply with [RFC 1918](https://tools.ietf.org/html/rfc1918) for best practices.
</details>

<details>
 <summary>Enabling access to private clusters</summary>

```bash
gcloud container clusters update [YOUR PRIVATE CLUSTER] \
    --zone [ZONE]
    --enable-master-authorized-networks \
    --master-authorized-networks [SOURCE CIDR RANGE]
```
</details>

### Viewing Cluster Information and Getting Credentials (gcloud)
<details>
 <summary>Describing the cluster</summary>
 
```bash
gcloud container clusters describe [YOUR CLUSTER] --zone [ZONE]
```
 </details>

<details>
 <summary>Getting the credentials from the cluster</summary>
 
```bash
gcloud container clusters get-credentials [YOUR CLUSTER] --zone [ZONE]
```

 Before you can interact with your cluster, you must get the credentials using this command.
</details>

### Interacting with your cluster (kubectl)
<details>
 <summary>Get all running resources in a cluster</summary>
 
```bash
kubectl get all
```
</details>

<details>
 <summary>Get all resources by type</summary>
 
```bash
kubectl get pods
kubectl get deployments
kubectl get services
kubectl get replicasets
kubectl get statefulsets
```
Run `kubectl api-resources` to display list of resources types in Kubernetes
</details>

<details>
 <summary>Get all resources across all namespaces</summary>
 
```bash
kubectl get all --all-namespaces
```
Run `kubectl api-resources` to display list of resources types in Kubernetes. Use `--namespace=[NAMESPACE]` to view resources in a specific namespace.
</details>

<details>
 <summary>Describe all resources by type</summary>
 
```bash
kubectl describe pod [POD NAME]
kubectl describe deployment [DEPLOYMENT NAME]
kubectl describe service [SERVICE NAME]
kubectl describe replicaset [REPLICASET NAME]
kubectl describe statefulset [STATEFULSET NAME]
```
Run `kubectl api-resources` to display list of resources types in Kubernetes
</details>

<details>
 <summary>Display logs of a pod/deployment</summary>
 
```bash
kubectl logs [POD/DEPLOYMENT NAME]
```
</details>

### Run/Create a Kubernetes resource

<details>
 <summary>Run a basic single container</summary>
 
```bash
kubectl run [NAME] --image=[IMAGE]
kubectl run nginx-sample --image=nginx
```
This creates a deployment rather than a pod. A deployment can be updated and scaled. A pod, on its own, cannot do that.
</details>

<details>
 <summary>Create a resource based on a definition file</summary>
 
```bash
kubectl create -f [RESOURCE DEFINITION FILE | YAML | JSON]
```
This creates and runs a resource based on the definition file specified (it can be a pod, service, deployment, replicaset, etc)
</details>

