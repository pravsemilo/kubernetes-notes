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
		* Functions
			1. Initialize a node with cloud specific region / zone labels.
			2. Initialize a node with cloud specific instance details like size, type etc.
			3. Obtain the node's network address, hostname etc.
			4. Handle node deletion issues.
		## Route controller
		* Responsible to configure routes in the cloud so that containers can communicate with each other.
		* Applicable only for Google Compute Engine.
		## Service controller
		* Responsible for listening to service events.
		* Based on the current state of services, it configures cloud load balancers.
		* Ensure that service backends are up to date.
		## PersistentVolumeLables controller
		* Applies labels to to volumes when created.
		* Labels are essential for scheduling of pods.
			* Volumes are constrained to work only in the region that they are in.
			* Any pod using these volumes should be in the same zone.
		* This was created specifically for CCM. Done to move the PV labelling logic from K8s apiserver to CCM.
2. Kubelet
	* Node controller contains the cloud dependent functionality of the kubelet.
	* Earlier kubelet was responsible for intializing a node with cloud specific details.
	* With CCM this functionality is moved from kubelet to CCM.
	* Approach
		* kubelet initializes a node without cloud-specific information.
		* kubelet adds a taint to newly created node that makes the node unschedulable.
		* CCM initializes the node with cloud specific information.
		* CCM removes the taint.
# References
* https://kubernetes.io/docs/concepts/architecture/cloud-controller/
