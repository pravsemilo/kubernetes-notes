* K8s approaches networking somewhat differently than Docker does by default.
* There are 4 distinct problems to be solved.
	1. Highly-coupled container-to-container communications. This is solved by `pod` and `localhost` communication.
	2. Pod-to-pod communications
	3. Pod-to-service communications. This is solved by `services`.
	4. External-to-service communications. This is solved by `services`.
# Summary
* Pods can communicate with other pods regardless of the host they land on.
* Every pod gets its own IP address.
* Hence we don't need to create link between pods.
* We never need to deal with mapping container ports to host ports.
* This creates a clean, backwards-compatible model where pods can be treated much like VMs or physical hosts from the perspective of port allocation, naming, service discovery, load balancing, application configuration and migration.
# Docker model
* By default, docker uses host-private networking.
* It creates a virtual bridge, called `docker0` by default, and allocates a subnet from one of the private address blocks.
* For each container that docker creates, it allocates a virtual ethernet device called `veth` which is attached to the bridge.
* `veth` is mapped to appear as `eth0` in the container using Linux namespaces.
* The in-container `eth0` interface is given an IP address from the bridge's address range.
* Hence docker container can talk to each other only if they are on the same machine, and thus the same virtual bridge.
* For docker containers to communicate across hosts, there must be allocated ports on the host's IP address which are then forwarded to the containers.
# Kubernetes model
* Issues with docker model
	* Coordinating ports across multiple developers is difficult to do at scale.
	* Dynamic port allocations bring application level complexity.
* K8s imposes the following fundamental requirements on any networking implementation :
	* All containers can communicate with all other containers without NAT.
	* All nodes can communicate with all containers and vice versa without NAT.
	* The IP that a container sees itself as is the same IP that others see it as.
* This implies that you can not just take two computers running docker and expect K8s to work. You must ensure that fundamental requirements are met.
* This model is less complex.
* Compatible with desire for K8s to enable low-friction porting of apps from VMs to containers.
* _IP-per-pod Model_
	* IPs are applied at `Pod` scope - containers within a `Pod` share their network namespace.
	* Containers within a `Pod` can reach each other's port on `localhost`.
	* This is implemented, using Docker as a _pod container_ which holds network namespace open, while app containers join that namespace using Docker's `--net=container:<id>`.
# References
* https://kubernetes.io/docs/concepts/cluster-administration/networking/
