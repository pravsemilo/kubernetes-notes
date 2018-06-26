* Pod is the smallest deployable object in K8s object model.
# Understanding Pods
* Basic building block of K8s.
* Smallest and simplest object that can be created / destroyed.
* Represents a running process in your cluster.
* Encapuslates an application container (or in some cases multiple containers), a storage resource, a unique network IP and options that govern how the container(s) should run.
* Represents a unit of deployment : _a single instance of an application in K8s_, which might consist of either a single container or a small number of containers that are tightly coupled and share resources.
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
	## [The Distributed System Toolkit : Patterns for Composite Containers](https://kubernetes.io/blog/2015/06/the-distributed-system-toolkit-patterns/)
	* Containers have become increasingly popular ways to package and deploy code.
	* Containers solve real-world problems with existing packaging and deployment tools.
	* Container offer us an opportunity to rethink the way we build distributed applications.
	* Just as SOA encouraged decomposition of an application to modular focused services, containers encourage further decomposition of services into closely cooperating modular containers.
	* By virtue of establishing a boundary, containers enable users to build their services using modular, reusable components, which in turn lead to services that are more reliable, scalable and faster to build than applications built from monolithic containers.
	* Abstraction layer provided by container image has great deal in common with abstraction boundary of class in object oriented programming.
	* Just like the right way to code is the separation of concerns into modular objects, right way to package applications is separation of concerns into modular containers.
	* This means breaking up not just the overall application, but also pieces within any one server into multiple modular containers that are easy to parameterize and reuse.
	* This way, most application developers can compose together modular containers written by others and build applications more quickly.
	* Modular containers provide the following :
		* Speed application development, since containers can be reused.
		* Codify expert knowledge since everyone collaborates on a single containerized implementation that reflects best practices.
		* Enable agile teams since container boundary is a natural boundary and contract for team responsibilities.
	* Provide separation of concerns and focus on specific functionality that reduces sphagetti dependencies and untestable components.
	* Building an application from modular containers means thinking about symbiotic groups of containers that cooperate to provide a service, not one container per service. 
	* In K8s, this symbiotic group of containers is called a pod. This also required that the containers of a pod be co-scheduled onto the same machine. The way to achieve this is to make pod itself as the atomic scheduling unit.
	### Patterns
	* In all of these cases we have used container boundary as an encapsulation / abstraction boundary.
	* This allowed to build modular and reusable components that we can combine to build applications.
		#### Sidecar containers
		* Extend and enhance the main container.
		#### Ambassador containers
		* Proxy a local connection to the world.
		* Example : An ambassador is a proxy responsible for splitting reads and writes and sending them to appropriate servers.
		#### Adapter containers
		* Standardize and normalize output.
		* Example : Transforming monitoring data from various containers into a single unified representation.
	## [Container Design Patterns](https://kubernetes.io/blog/2016/06/container-design-patterns/)
* Each pod is meant to run a single instance of the application.
* To scale horizantally, you should use multiple pods.
* This is referred as _replication_ in K8s.
* Replicated pods are created and managed as a group by an abstraction called controller. 
## How Pods manage multiple Containers
* Pods are designed to support multiple cooperating processes as containers that form a cohesive unit of service.
* Containers in a pod are automatically co-located and co-scheduled on the same machine.
* Containers can share resources and dependencies, communicate with one another and coordinate when and how they are terminated.
### Networking
* Each pod is assigned a unique IP address.
* Every container in the pod shares the network namespace including the IP address and network ports.
* Containers within the same pod can communicate via localhost.
### Storage
* Pod can specify a set of shared storage volumes.
* All containers in the pod have access to the volumes.
* Volumes also allow persistent data in a pod to survive in case of container restarts.
# Working with Pods
* Pods are not created directly. This is because pods are designed as ephemeral, disposable entities.
* When a pod gets created (by you or by a controller), it is scheduled to run on a node in your cluster.
* Pod remains in that node until the process is terminated, pod object is deleted, pod is evicted for lack of resources or the node fails.
* Restarting a containers is not same as restarting the pod. Pod itself doesn't run, but is an environment the container runs in and persists until it is deleted.
* Pods do not by themselves self heal.
* If a pod is scheduled on a node that fails or scheduling operation itself fails, the pod is deleted.
* Similarly a pod won't survive an eviction due to lack of resources or node maintenance.
* K8s uses a higher level abstraction, called _Controller_, that handles the work of managing the relatively disposable pod entities.
* Thus while it is possible to use the pod directly, it is far more common in K8s to manage pods using a controller.
## Pods and Controller
* A controller can create and manage multiple pods for you, handling replication and rollout and providing self healing capabilites.
* Some controllers that contain one or more pods include :
	* `Depoloyment`
	* `StatefulSet`
	* `DaemonSet`
* In general, Controllers use a `Pod Template` that you provide to create the pods for which it is responsible.
# Pod Templates
* Pod templates are pod specifications which are included in other object like `Replication Controllers`, `Jobs` and `DaemonSets`.
* Controllers use pod templates to create pods.
* Pod templates are like cookie cutters. Once the cookie has been cut, it has not relationship to the cutter.
* Hence any change to pod template doesn't change pods already created.
* On the other hand pods specify the current desired state of all containers belonging to the pod.
# References
* https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/
* https://kubernetes.io/blog/2015/06/the-distributed-system-toolkit-patterns/
* https://kubernetes.io/blog/2016/06/container-design-patterns/
