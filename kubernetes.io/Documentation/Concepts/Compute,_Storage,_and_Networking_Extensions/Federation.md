* `Federation V1`
	* Reuses K8s API resources as is.
	* Alpha
* `Federation V2`
	* Dedicated federation API apart from K8s API.
# Why federation
* Federation makes it easy to manage multiple clusters.
* Federation helps to  acheive :
	* Sync resources across clusters - Provides ability to keep resources in multiple clusters in sync. Eg. - Same deployment exists in multiple clusters.
	* Cross cluster discovery - Ability to auto-configure DNS servers and load balancers with backends from all clusters.
	* High Availability - By spreading load across clusters and auto configuring DNS servers and load balancers, federation minimises the impact of cluster failure.
	* Avoiding provider lock-in - By making it easier to migrate applications across clusters, federation prevents cluster provider lock-in.
* Reasons to have multiple clusters :
	* Low Latency - Serve users from the cluster closer to them.
	* Fault Isolation - Better to have multiple small clusters rather than a single large cluster for fault isolation.
	* Scalability
	* Hybrid Cloud
## Caveats
* Increased network bandwidth
* Increased costs
* Reduced cross cluster isolation - Any bug in federation control plane impacts all clusters. This is mitigated by keeping the logic in federation control plane to a minimum. It mostly delegates to control plane in K8s clusters whenever it can. Also design and implementation errs on the side of safety and avoiding multi-cluster outage.
* API maturity
## Hybrid cloud capabilities
* `kubefed` is the recommended way to deploy federated clusters.
# Setting up federation
* To be able to federate multiple clusters, you first need to setup a federation control plane.
# API resources
* Once you have the federation control plane set up, you can start creating federated API resources.
# Cascading deletion
* K8s 1.6 supports cascading deletion of federated resources.
* Not enabled by default when using REST API.
* Enabled by default in `kubectl delete`.
# Scope of a single cluster
* All VMs in a K8s cluster should be in same availability zone.
	* Compared to having a single global cluster, there are single points of failure.
	* Easier to reason about the availability properties of a single-zone cluster.
* Preferred to run fewer clusters with more VMs per zone.
	* Improved bin packing of Pods if more nodes in one cluster (less resource fragmentation).
	* Reduced operational overhead.
# References
* https://kubernetes.io/docs/concepts/cluster-administration/federation/
