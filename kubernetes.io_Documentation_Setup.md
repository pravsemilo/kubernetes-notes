# Picking The Right Solution
  * Can run on various platforms like laptop, VM, bare metal servers etc.
## Local Machine Solutions
  * `Minikube` - Ideal for local single node cluster for development and testing.
  * `Kubeadm-dnd` - Multi node K8s cluster which only requires a docker daemon. User docker-in-docker technique to spawn the cluster.
  * `Ubuntu on LXD` - Support a nine instance deployment on localhost.
## Hosted Solutions
  * Google Kubernetes Engine
  * AWS ECS
  * Azure Container Service
  * OpenShift
  * Kubermatic
## Turnkey Cloud Solutions
  * Google Compute Engine
  * AWS
  * Azure
## On-premise Turnkey Solutions
  * IBM Cloud Private
  * Kubermatic
# Running Kubernetes Locally Via Minikube