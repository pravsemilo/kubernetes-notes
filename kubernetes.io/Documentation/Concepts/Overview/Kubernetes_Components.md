# Master Components
* Provide the cluster's control plane.
* Make global decision about the cluster.
* Detect and respond to cluster events.
* Though can be run on any machine in the cluster, for simplicity all master components start in the same machine.
	* Avoid running user containers in this machine.
## kube-apiserver
* Exposes the K8s API.
* Front end for K8s control plane.
* Can scale horizantally.
## etcd
* Consistent and highly-available key-value store.
* Used as backing store for all cluster data.
* Always have a backup plan for etcd's data in your cluster.
## kube-scheduler
* Watches newly created pods that have no node assigned.
* Selects a node for them to run on based on individual and collective resource requirements, hardware / software / policy constraints, affinity and anti-affinity specifications, data locality and deadlines.
## kube-controller-manager
* Runs controllers.
* Logically each controller is a separate process, but for simplicity they are all compiled into a single binary and run in a single process.
* These controllers include :
	* _Node Controller_ - Responsible for noticing and responding when nodes go down.
	* _Replication Controller_ - Responsible for maintaining the correct number of pods for every replication controller object in the system.
	* _Endpoints Controller_ - Populates the Endpoint object (joins Services and Pods).
	* _Service Account & Token Controllers_ - Create default account and API access tokens for new namespaces.
## cloud-controller-manager
* Runs controllers that interact with the underlying cloud providers.
* Runs cloud-provider specific controller loops only.
* Allows cloud vendors code and the K8s core to evolve independent of each other.
# Node Components
* Run on every node.
* Responsible for maintaining running pods.
* Provide the K8s runtime.
## kubelet
* Makes sure that containers are running in a pod.
* Take a set of `PodSpecs` that are provided through various mechanisms and ensures that the containers described in these PodSpecs are running and healthy.
## kube-proxy
* Enables K8s service abstraction by maintaining network rules on the host and performing connection forwarding.
## Container Runtime
* Responsible for running containers.
* K8s supports Docker, rkt, runc and any OCI runtime-spec implementation.
# Addons
* Addons are pods and services that implement cluster features.
* These pods may be managed by Deployments, ReplicationControllers etc.
* Namespaced addons are created in `kube-system` namespace.
## DNS
* Required for all clusters.
* `ClusterDNS` is a DNS server which serves DNS records for K8s services.
* Containers started by K8s include this DNS in their DNS searches.
## Web UI (Dashboard)
* To manage and troubleshoot applications running in the cluster.
## Container Resource Monitoring
* Records generic time-series metrics about containers in a central store and provides a UI.
## Cluster-level Logging
* Responsbile for saving container logs to a central log store with search / browse interface.
# References
* https://kubernetes.io/docs/concepts/overview/components/
