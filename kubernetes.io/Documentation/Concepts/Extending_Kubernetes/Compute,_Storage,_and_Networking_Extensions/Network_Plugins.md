* Flavors of network plugins
	* CNI Plugins : Adhere to appc / CNI specification and hence interoperable.
	* Kubenet Plugin : Implements basic `cbr0` using the `bridge` and `host-local` CNI plugins.
# Installation
* kubelet has a single default network plugin and a default network common to entire cluster.
* It probes for plugin at startup, remembers what it found and executes the selected plugin at appropriate times in the pod lifecycle.
* Command line params
	* `cni-bin-dir` : Which directory to probe for plugins?
	* `network-plugin` : The plugin to use from `cni-bin-dir`.
# References
* https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/
