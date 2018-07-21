# Overview
* To work with Kubernetes, you use _Kubernetes API objects_ to describe your cluster’s _desired state_:
	* What applications or what other workloads you want to run?
	* What container images they use?
	* The number of replicas.
	* What network and disk resources you want to make available.
* You set your desired state by creating objects using the Kubernetes API :
	* `kubectl` command line
	* Kubernetes API
* Once you’ve set your desired state, the _Kubernetes Control Plane_ works to make the cluster’s current state match the desired state. It performs the following tasks automatically.
	* Start and restart containers.
	* Scaling the number of replicas of a given application.
* Kubernetes Control Plane consists of a collection of processes running on your cluster.
	* __Kubernetes Master__ : Collection of three processes that run on a single node in your cluster designated as the master node.
		* `kube-apiserver`
		* `kube-controller-manager`
		* `kube-scheduler`
	* Each individual non-master node in your cluster runs two processes.
		* `kubelet` - Communicates with Kubernetes master.
		* `kube-proxy` - A network proxy which reflects K8s networking services on each node.
# Kubernetes Objects
* Kubernetes contains a number of abstractions that represent the state of your system.
* These abstractions are represented by objects in the Kubernetes API.
* Basic K8s objects
	* __Pod__
	* __Service__
	* __Volume__
	* __Namespace__
* Kubernetes contains a number of higher-level abstractions called _Controllers_. Controllers build upon the basic objects, and provide additional functionality and convenience features.
* Some of the common Controllers are
	* __ReplicaSet__
	* __Deployment__
	* __StatefulSet__
	* __DaemonSet__
	* __Job__
# Kubernetes Control Plane
* Governs how K8s communicates with your cluster.
* Maintains a record of all of K8s objects in the system.
* Runs continous control loop to manage the state of objects.
* Control loops will respond to changes in cluster and work to make the actual state of all objects in the system match the desired state.
## Kubernetes Master
* Responsible for maintaining the desired state of your cluster.
* Refers to a collection of processes.
* Typically these processes run on the same node called the master node.
* Master node can also be replicted for availability and redundancy.
## Kubernetes Nodes
* Machines that run your applications and cloud workflows.
* They are controlled by master. You don't directly interact with them.
# References
* https://kubernetes.io/docs/concepts/
