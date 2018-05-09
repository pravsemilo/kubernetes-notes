# What is Kubernetes?
* K8s is a portable, extensible open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation.
## Why do I need Kubernetes and what can it do?
* K8s can be thought of as
	* Container Platform
	* Microservices Platform
	* Portable Cloud Platform
* Provides a container-centric management environment.
* Orchestrates computing, network and storage infrastructure on behalf of user workloads.
* Enables portability across infrastructures provides.
* Provides simplicity of PaaS with flexibility of IaaS.
## How is Kubernetes a platform?
* _Labels_ empower users to organize their resources however they please.
* _Annotations_ enable users to decorate resources with custom information to facilitate their workflows and provide an easy way for management tools to checkpoint state.
* Kubernetes control plane is built upon the same APIs that are available to developers and users. Users can write their own controllers, such as schedulers, with their own APIs that can be targeted by a general-purpose command-line tool.
* This design has enabled a number of other systems to build atop Kubernetes.
## What Kubernetes is not?
* K8s is not a traditional, all-inclusive PaaS.
* It provides some generally applicable features common to PaaS offerings, such as deployment, scaling, load balancing, logging, and monitoring.
* K8s provides the building blocks for building developer platforms, but preserves user choice and flexibility where it is important.
* Does not limit the types of applications supported.
* Does not deploy source code and does not build your application.
* Does not dictate logging, monitoring, or alerting solutions. It provides some integrations as proof of concept, and mechanisms to collect and export metrics.
* Does not provide application-level services, such as middleware, database, cache etc.
* Does not provide nor mandate a configuration language / system (e.g., jsonnet). It provides a declarative API that may be targeted by arbitrary forms of declarative specifications.
* Does not provide nor adopt any comprehensive machine configuration, maintenance, management or self-healing systems.
* K8s is not a mere orchestration system. In fact, it eliminates the need for orchestration.
* In contrast, K8s is comprised of a set of independent, composable control processes that continuously drive the current state towards the provided desired state.
# Kubernetes Components
## Master Components
* Provide the cluster's control plane.
* Make global decision about the cluster.
* Detect and respond to cluster events.
* Though can be run on any machine in the cluster, for simplicity all master components start in the same machine.
	* Avoid running user containers in this machine.
### kube-apiserver
* Exposes the K8s API.
* Front end for K8s control plane.
* Can scale horizantally.
### etcd
* Consistent and highly-available key-value store.
* Used as backing store for all cluster data.
* Always have a backup plan for etcd's data in your cluster.
### kube-scheduler
* Watches newly created pods that have no node assigned.
* Selects a node for them to run on based on individual and collcetive resource requirements, hardware / software / policy constraints, affinity and anti-affinity specifications, data locality and deadlines.
### kube-controller-manager
* Runs controllers.
* Logically each controller is a separate process, but for simplicity they are all compiled into a single binary and run in a single process.
* These controllers include :
	* _Node Controller_ - Responsible for noticing and responding when nodes go down.
	* _Replication Controller_ - Responsible for maintaining the correct number of pods for every replication controller object in the system.
	* _Endpoints Controller_ - Populates the Endpoint object (joins Services and Pods).
	* _Service Account & Token Controllers_ - Create default account and API access tokens for new namespaces.
### cloud-controller-manager
* Runs controllers that interact with the underlying cloud providers.
* Runs cloud-provider specific controller loops only.
* Allows cloud vendors code and the K8s core to evolve independent of each other.
## Node Components
* Run on every node.
* Responsible for maintaining running pods.
* Provide the K8s runtime.
### kubelet
* Makes sure that containers are running in a pod.
* Take a set of `PodSpecs` that are provided through various mechanisms and ensures that the containers described in these PodSpecs are running and healthy.
### kube-proxy
* Enables K8s service abstraction by maintaining network rules on the host and performing connection forwarding.
### Container Runtime
* Responsible for running containers.
* K8s supports Docker, rkt, runc and any OCI runtime-spec implementation.
## Addons
* Addons are pods and services that implement cluster features.
* These pods may be managed by Deployments, ReplicationControllers etc.
* Namespaced addons are created in `kube-system` namespace.
### DNS
* Required for all clusters.
* `ClusterDNS` is a DNS server which serves DNS records for K8s services.
* Containers started by K8s include this DNS in their DNS searches.
### Web UI (Dashboard)
* To manage and troubleshoot applications running in the cluster.
### Container Resource Monitoring
* Records generic time-series metrics about containers in a central store and provides a UI.
### Cluster-level Logging
* Responsbile for saving container logs to a central log store with search / browse interface.
# References
* https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/
* https://kubernetes.io/docs/concepts/overview/components/
