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
 <summary>Creating a private cluster</summary>

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

<p>Creating a private cluster must comply with [RFC 1918](https://tools.ietf.org/html/rfc1918)</p>
</details>