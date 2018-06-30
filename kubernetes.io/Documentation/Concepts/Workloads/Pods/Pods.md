* Pods are the smallest deployable units of computing that can be created and managed in K8s.
# What is a Pod?
* A pod is a group of containers with shared storage / network and a specification for how to run the containers.
* A pod's content are always co-located and co-scheduled and run in a shared context.
* A pod models an application-specific "logical host". It contains one or more application containers which are relatively tightly coupled - in a pre-container world, they would have executed on the same machine.
* The shared context of a pod is a set of Linux namespaces, cgroups and potentially other facets of isolation.
* Within a pod's context, the individual applications may have further isolations applied.
* Containers within a pod share an IP address and port space.
* Containers can find each other via localhost. They can also communicate using standard IPC like SystemV semaphores or POSIX shared memory.
* Containers in different pods have distinct IP addresses and cannot communicate via IPC without special configuration. These containers usually communicate via pod's IP address.
* Containers within a pod also have access to shared volumes. These are made available to be mounted into each container's filesystem.
* Pods are relatively ephemeral entities.
* Pods are created, assigned a unique ID and scheduled to nodes where they remain until termination or deletion.
* If a node dies, the pods on that node are scheduled for deletion after a timeout.
* A given pod, as defined by a UID, is not rescheduled to a new node. Instead it can be replaced by an identical pod with even the same name, but with a new UID.
* When something is said to have the same lifetime as a pod, such as a volume, that means that it exists as long as that pod (with that UID exists). If that pod is deleted for any reason, even if an identical replacement is created, the related thing is also destroyed and created new.
# Motivation for pods
# References
* https://kubernetes.io/docs/concepts/workloads/pods/pod/
