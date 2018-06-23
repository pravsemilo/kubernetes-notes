# Resource
* An endpoint in the _K8s API_ that stores a collection of _API objects_ of a certain kind.
# Custom Resources
* Extensions of K8s API that is not necessarily available on every cluster.
* Represents a customization of a particualar K8s installation.
* Dynamically registered and independently updated of the cluster.
* Can be accessed via `kubectl`.
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
## Declarative APIs
* Your API consists of a relatively small number of relatively small objects (resources).
* The objects define configuration of applications or infrastructure.
* The objects are updated relatively infrequently.
* Humans often need to read and write the objects.
* The main operations on the objects are CRUD.
* Transactions across objects are not required.
## Imperative APIs
* Opposite of declarative.
* Synchronous response.
* Separate operation to check request status.
* Directly store large amount of data per request.
* Natural operations on objects are not CRUD.
* API is not easily modeled as resources.
## ConfigMap vs Custom Resource
* Use ConfigMap if :
	* There is an existing, well documented file format.
	* You want to put entire config file as a key in a configMap.
	* Main use of config file is for a program to configure itself.
	* You want to perform rolling updates via _Deployments_, etc, when file is updated.
* Use a custom resource (CRD or aggregated API) if :
	* You want to use K8s client libraries and CLIs to create and update new resources.
	* You want top-level support from _kubectl_.
	* You want to build automation that watches for updates and acts on them.
	* You want to use K8s api conventions.
	* You want the object to be an abstraction over a collection of controlled resources or a summarization of other resources.
# Adding Custom Resources
* CRDs allow users to create new type of resources without adding another _APIServer_.
* Aggregated APIs are subordinate _APIServers_ that behind the primary API server, which acts as a proxy. This is called _API Aggregation (AA)_.
* Regardless of whether they are installed via CRDs or AA, the new resources are called _Custom Resources_ to distinguish them from built-in K8s resources.
# CustomResourceDefinitions (CRDs)
* Easier to use.
* Doesn't require programming in some cases.
* _CustomerResourceDefinition (CRD)_ API resource allows you to define custom resources.
* Defining a CRD object creates a new custom resource with a name and schema that you specify.
* K8s API serves and handles the storage of your custom resource.
* Successor of `ThirdPartyResource (TPR)` API and available as of K8s 1.7.
# API Aggregation
* Requires programming.
* More control over API behavior like how data is stored, conversion between API versions etc.
* Allows you to provide specialized implementations for your custom resources by writing and deploying your own standalone API server.
# Choosing a method for adding custom resources
* CRDs are easier to use.
* Aggregated APIs are more flexible.
* User CRDs if,
	* You have a handful of fields.
	* You are using the resource within your company as opposed to a commerical product.
## Ease Of Use
* CRDs don't require programming. CRD can be written in any language. On the other hand, AAs need to be written in Go.
* CRs are handled by API server and hence don't need any additional service. On the other hand AA's need an additonal service to be created that could fail.
* No ongoing support once the CRD is created. Any bug fixes are picked up as part of normal Kubernetes Master upgrades. AAs may need to periodically pickup bug fixes from upstream and rebuild and update the Aggregated APIserver.
# Common Features
* When you create a CR, either via CRD or AA, you get many features for your API.
	* CRUD
	* Watch
	* Discovery
	* json-patch
	* merge-patch
	* HTTPS
	* Built-in authentication
	* Built-in authorization
	* Finalizers
	* UI / CLI display
	* Unset vs empty fields
	* Labels and annotations
# Preparing to install a custom resource
## Third party code and new points of failure
* Installing an Aggregated APIserver always involves running a new Deployment.
## Storage
* Irrespective of whether we use CRDs or AAs, creating resources involves consuming storage space.
## Authentication, authorization and auditing
* CRDs always use the same authentication, authorization and audit logging as built-in resources of your API Server.
* If you use RBAC for authorization, you may need to grant access explicity for your new resources.
* Aggregated API servers may or may not use the same authentication, authorization and auditing as the primary API server.
# Accessing a custom resource
* `kubectl`
* K8s dynamic client
* Your own REST client
* A client generated using K8s client generation tools.
# References
* https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/
