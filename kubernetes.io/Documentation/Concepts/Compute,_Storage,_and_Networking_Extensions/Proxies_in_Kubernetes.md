# Proxies
* There are several different proxies that you encounter when using K8s.
	* `kubectl proxy`
		* Runs on user's desktop or in a pod.
		* Proxies from localhost to K8s `apiserver`.
		* Client to proxy is HTTP.
		* Proxy to `apiserver` is HTTPS.
		* Locates `apiserver`.
		* Adds authentication headers.
	* `apiserver proxy`
		* Bastion built on `apiserver`.
		* Connects a user outside of cluster to cluster IPs which are otherwise unreachable.
		* Runs in `apiserver` processes.
		* Client to proxy is HTTPS.
		* Proxy to `apiserver` may be HTTP or HTTPS.
		* Can be used to reach a `Pod`, `Node` or `Service`.
		* Does loadbalancing when used to reach a `Service`.
	* `kube proxy`
		* Runs on each node.
		* Proxies UDP and TCP.
		* Does not understand HTTP.
		* Provides load balancing.
		* Just used to reach services.
	* Proxy / Load Balancer in front of `apiserver(s)`
		* Varies from cluster to cluster.
		* Sits between all clients and `apiservers`.
	* Cloud Load Balancer on external services
		* Provided by cloud provider.
		* Created automatically when K8s service type is `LoadBalancer`.
		* Uses UDP/TCP only.
# References
* https://kubernetes.io/docs/concepts/cluster-administration/proxies/
