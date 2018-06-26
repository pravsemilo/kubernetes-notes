* Pod is the smallest deployable object in K8s object model.
# Understanding Pods
* Basic building block of K8s.
* Smallest and simplest object that can be created / destroyed.
* Represents a running process in your cluster.
* Encapuslates an application container (or in some cases multiple containers), a storage resource, a unique network IP and options that govern how the container(s) should run.
* Represents a unity of deployment : _a single instance of an application in K8s_, which might consist of either a single container or a small number of containers that are tightly coupled and share resources.
* Docker is the most common container runtime.
* Support for other container runtimes is also provided.
* Pods are used in two ways.
	* __Pods that run in a single container__
		* "One container per pod"
		* Think of pod as a wrapper over a single container.
		* K8s manages the pod rather than the container directly.
	* __Pods that run multiple containers that need to work together__
		* Pod encapsulates an application composed of multiple co-located containers which are tightly coupled and share resources.
		* These containers might form a single cohesive unit of a service.
		* Pod wraps these containers and storage resources as a single manageable entity.
* Additional information on pod use cases
	# The Distributed System Toolkit : Patterns for Composite Containers
	# Container Design Patterns
# References
* https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/
