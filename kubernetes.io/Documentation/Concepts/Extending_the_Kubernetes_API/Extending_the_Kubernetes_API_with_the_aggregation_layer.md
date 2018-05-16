# Aggregation Layer
* Allows K8s to be extended with additional APIs.
* Enables installing additional Kubernetes-style APIs in your cluster.
* These can either be pre-built, existing 3rd party solutions, such as `service-catalog`, or user-created APIs like `apiserver-builder`.
* In 1.7 the aggregation layer runs within _kube-apiserver_.
* To register an API :
	* User must add an `APIService` object, which claims the URL path in K8s API.
	* Aggregation layer will proxy that path to the registered `APIService`.
	* APIService will be implemented by an `extension-apiserver` in a pod running in the cluster.
	* This extension-apiserver will need to be paired with one or more controllers if active management of the resource is needed.
	* `apiserver-builder` provides a skeleton for both.
# References
* https://kubernetes.io/docs/concepts/api-extension/apiserver-aggregation/
