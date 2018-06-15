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
	`OutOfDisk`|Is there sufficient space for addding new pods?
# References
* https://kubernetes.io/docs/concepts/architecture/nodes/
