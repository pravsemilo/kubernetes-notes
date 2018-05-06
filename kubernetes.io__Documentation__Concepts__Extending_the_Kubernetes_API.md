# Resource
* An endpoint in the _K8s API_ that stores a collection of _API objects_ of a certain kind.
# Custom Resources
* Extensions of K8s API that is not necessarily available on every cluster.
* Represents a customization of a particualar K8s installation.
* Dynamically registered and independently updated of the cluster.
* Can be accessed via _kubectl_.
## Custom Controllers
* On their own, custom resources simply let you store and retrieve structured data.
* It is only when combined with a _controller_ that they become a true declarative API.
* The controller interprets the structured data as a record of the user’s desired state, and continually takes action to achieve and maintain that state.
* _Custom controller_ is a controller that users can deploy and update on a running cluster, independently of the cluster’s own lifecycle.
* Can work with any kind of resource, but they are especially effective when combined with custom resources.
## API Aggregation vs Stand-alone API
API Aggregation|Stand-alone API
---------------|---------------
API is declarative.|API doesn't fit the declarative model.
Your new types are read and written via _kubectl_.|_kubectl_ support is not required.
Want to view your new types via K8s UI.| K8s UI support is not required.
Developing a new API.|Already have a program that serves your API.
Willing to accept the format restriction that K8s put on REST resource paths.|You need to have specific REST paths to be compatible with existing REST APIs.
Resources are naturally scoped to a cluster or the namespace of a cluster.|Cluster or namespaced resources are a poor fit.
# Aggregation Layer
* Allows K8s to be extended with additional APIs.
* In 1.7 the aggregation layer runs within _kube-apiserver_.
* To register an API :
	* User must add an `APIService` object, which claims the URL path in K8s API.
	* Aggregation layer will proxy that path to the registered `APIService`.
	* APIService will be implemented by an `extension-apiserver` in a pod running in the cluster.
	* This extension-apiserver will need to be paired with one or more controllers if active management of the resource is needed.
	* `apiserver-builder` provides a skeleton for both.
# References
* https://kubernetes.io/docs/concepts/api-extension/custom-resources/
* https://kubernetes.io/docs/concepts/api-extension/apiserver-aggregation/
