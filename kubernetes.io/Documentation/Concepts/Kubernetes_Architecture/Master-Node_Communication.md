# Overview
* Intent is to document the communcation path between master (apiserver) and K8s cluster.
* Allow users to customize their installation to harden the network configuration such that cluster can run on an untrusted network.
# Cluster -> Master
* All communication paths from cluster to master terminate at apiserver.
* None of the master components are designed to expose remote services.
* In a typical deployment :
	* apiserver listens on 443 for remote connections.
	* Client authentication is enabled.
	* Authorization should be enabled if anonymous reuqests or service account tokens are allowed.
* Nodes should be provisioned with public root certificate for the cluster.
* Pods that wish to connect to apiserver can do so with service account.
	* K8s will automatically inject the public root certificate and a valid bearer token while pod instantiation.
	* The `kubernetes` service (in all namespaces) is configured with a virtual IP address that is redirected via kube-proxy to apiserver's HTTPS endpoint.
* Master components also communicate with apiserver over the secure port.
# Master -> Cluster
## apiserver -> kubelet
* Use Cases
	* Fetching logs for pods.
	* Attaching to running pods.
	* Providing the kubelet's port forwarding functionality.
* Communication terminates at kubelet's HTTPS endpoint.
* apiserver doesn't verify kubelet's certificate. Use `--kubelet-certificate-autority` to use a root certificate bundle.
* Kubelet authentication and authorization can be enabled for security.
## apiserver -> nodes, pods or services
* Plain HTTP
* Can be prefixed with `https:` but certificates will not be validated.
* Not safe to run over public / untrusted networks.
# References
* https://kubernetes.io/docs/concepts/architecture/master-node-communication/
