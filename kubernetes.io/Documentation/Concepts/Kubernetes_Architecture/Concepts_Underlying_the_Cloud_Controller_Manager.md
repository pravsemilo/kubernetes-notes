# Cloud Controller Manager (CCM)
* Not to be confused with the binary. This is about the concept.
* Created to allow cloud specific vendor code and K8s core to evolve independent of one another.
* Runs alongside other master components.
* Can also be run as an addon.
* Design is based on plugin mechanism that allows new cloud providers to integrate.
# Components of CCM
* Breaks away some functionality of K8s controller manager and runs as a separate process.
* Following controllers are run by CCM instead of K8s controller manager : 
	* Node controller
	* PersistentVolumeLabels controller
	* Route controller
	* Service controler
# Functions of the CCM
1. Kubernetes controller manager
* CCM runs the following control loops.
	## Node controller
	* Initalizing a node by obtaining information about the nodes running in the cluster from the cloud provider.
	* Funcations
		1. Initialize a node with cloud specific region / zone labels.
		2. Initialize a node with cloud specific instance details like size, type etc.
		3. Obtain the node's network address, hostname etc.
		4. Handle node deletion issues.
	## Route controller
	## PersistentVolumeLables controller
# References
* https://kubernetes.io/docs/concepts/architecture/cloud-controller/
