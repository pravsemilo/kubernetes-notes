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
# References
* https://kubernetes.io/docs/concepts/architecture/nodes/
