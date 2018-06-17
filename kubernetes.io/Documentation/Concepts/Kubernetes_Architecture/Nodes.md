# What is a node?
* Worker machine in K8s.
* Previously known as `minion`.
* May be VM or physical machine.
* Has necessary services to run `pods`.
* Managed by master components.
* Services on a node include `Docker`, `kubelet` and `kube-proxy`.
# Node Status
* Contains the following information
	* `Address`
	* `Condition`
	* `Capacity`
	* `Info`
## Addresses
* Fields depend on cloud provider or bare metal configuration.
	* _HostName_
	* _ExternalIP_
	* _InternalIP_
## Condition
* `condition` field describes the status of all `Running` nodes.

Node Condition|Description
--------------|-----------
`OutOfDisk`|Is there sufficient space for adding new pods?
`Ready`|Is node healthy and ready to accept pods?
`MemoryPressure`|Is node memory running low?
`DiskPressure`|Is node disk space running low?
`NetworkUnavailable`|
`ConfigOK`|Is kubelet configured correctly?

* Node condition is represented as a JSON object.
* If the `Ready` condition is _Unknown_ or _False_ for longer than `pod-eviction-timeout`, an argument is passed to `kube-controller-manager` and all of the pods on that node are scheduled for deletion by `NodeController`.
* The default eviction timeout is 5 minutes.
* If the node is unreachable, `apiserver` is not able communicate with the `kubelet` on it. In such case the decision to delete cannot be communicated until communication is re-established to `apiserver`.
## Capacity
* Resources available like CPU, memory and maximum number of pods that can be scheduled.
## Info
* Kernel version, K8s version, Docker version, OS etc.
# Management
* Node is not inherently created by K8s.
* When we create a node, K8s is creating an object that represents the node.
* After creation, K8s will check if node is valid or not.
	* Health check based on node name.
	* Are all the necessary services running?
* If node is valid, it is elgible to run a pod. It will be ignored for any cluster activity till it becomes valid.
* K8s will keep the object for invalid node unless it is deleted.
## Node Controller
* A K8s master component which manages various aspects of nodes.
* Roles in a nodes life :
	* Assigning a CIDR block to the node when it is registered.
	* Keeping node controller's internal node list updated with cloud provider's list of available machines.
		* Whenever a node is unhealthy, the node controller asks the cloud provider if the VM for that node is still available.
		* If not, the node controller deletes the node from its list of nodes.
	* Monitor the node's health.
		* Update the _NodeReady_ condition of _NodeStatus_ to _ConditionUnkown_ when a node is unreachable.
		* Later evict all pods from the node if node is still unreachable.
## Self Registration of Nodes
* When the kubelet flag `--register-node` is true, kubelet will attempt to register with the API server.
* Currently kubelet is authorized to create/modify any node resource. In practice it only creates/modifies it's own.
### Manual Node Administration
* A cluster administrator can create or modify node objects.
* If the administrator wishes to create node objects manually, set the kubelet flag `--register-node=false`.
* Modification are irrespective of `--register-node` flag.
* Modifications can include setting labels and marking the node as unschedulable.
* Marking a node unschedulable will prevent new pods from being scheduled on that node. This won't affect existing pods.
```
$ kubectl cordon $NODENAME
```
* Pods created by DaemonSet controller bypass the K8s scheduler and hence don't respect the unschedulable attribute on a node.
## Node Capacity
* Capacity of node is part of node object.
* Nodes register themselves and report their capacity.
* In case of manual registration, node capacity is set while adding a node.
# References
* https://kubernetes.io/docs/concepts/architecture/nodes/
