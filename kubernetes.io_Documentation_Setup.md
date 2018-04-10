# Picking The Right Solution
* Can run on various platforms like laptop, VM, bare metal servers etc.
## Local Machine Solutions
* `Minikube` - Ideal for local single node cluster for development and testing.
* `Kubeadm-dind` - Multi node K8s cluster which only requires a docker daemon. User docker-in-docker technique to spawn the cluster.
* `Ubuntu on LXD` - Support a nine instance deployment on localhost.
## Hosted Solutions
* Google Kubernetes Engine
* AWS ECS for Kubernetes (EKS)
* Azure Container Service
* OpenShift
* Kubermatic - Provides managed K8s clusters for various public clouds, including AWS and Digital Ocean, as well as on-premises with OpenStack integration.
## Turnkey Cloud Solutions
* Google Compute Engine
* AWS
* Azure
## On-premise Turnkey Solutions
* IBM Cloud Private
* Kubermatic
## `kubeadm`
* If we already have a way to configure hosting resources, we can use kubeadm to bring up a cluster with a single command per machine.
# Running Kubernetes Locally Via Minikube
## `Minikube`
* Minikube is a tool that makes it easy to run K8s locally.
* Runs a single node K8s cluster inside a VM on your local machine.
### Features
* DNS
* NodePorts
* ConfigMaps & Secrets
* Dashboards
* Container Runtime - Docker / rkt / CRI-O
* Enabling CNI (Container Network Interface)
* Ingress
### Quickstart
* Supported Drivers
	* virtualbox
	* vmwarefusion
	* kvm
	* hyperkit
	* xhyve
* Commands
	* `minikube start` - Start your cluster. Creates and configures a virtual machine that runs a single node K8s cluster. This command also configures your kubectl installation to talk to this cluster.
		* `--vm-driver`
		* `--kubernetes-version`
		* `--network-plugin`
		* `--container-runtime`
		* `--bootstrapper`
		* `--extra-config`
	* `minikube ip`
	* `minikube get-k8s-versions`
	* `minikube stop` - Stop a cluster.
	* `minikube delete` - Delete the cluster, shutdown and delete the minikube virtual machine. No data is stored or preserved.
### Interacting With Your Cluster
* `kubectl`
	* `minikube start` command creates a `kubectl context` called "minikube". This context contains the configuration to communicate with your minikube cluster.
* Dashboard - `minikube dashboard`
* Services
	* `minikube service [-n namespace] [--url] NAME`
### Networking
* The minikube VM is exposed to the host system via a host-only IP address.
* IP address can be obtained via `minikube ip` command.
* Any services to type `NodePort` can be accessed over that IP address.
* To determine NodePort of your service
	* `kubectl get service $SERVICE --output='jsonpath="{.spec.ports[0].nodePort}"'`
### Persistent Volumes
* Supports PersistentVolumes of type `hostPath`.
* These PersistentVolumes are mapped to a directory inside minikube VM.
* minikube VM boots into a tmpfs, so data will not be persisted across reboots.
* However Minikube is configured to persist files stored under following host directories.
	* `/data`
	* `/var/lib/localkube`
	* `/var/lib/docker`
# References
* https://kubernetes.io/docs/setup/
* https://kubernetes.io/docs/setup/pick-right-solution/
* https://kubernetes.io/docs/getting-started-guides/minikube/
