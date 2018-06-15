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
# References
* https://kubernetes.io/docs/concepts/architecture/nodes/
