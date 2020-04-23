# CLI Commands for GKE

### Creating clusters
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

### Viewing Cluster Information and Getting Credentials
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