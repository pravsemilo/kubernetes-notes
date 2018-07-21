# Understanding Kubernetes Objects
* K8s objects are persistent entities in the K8s system.
* K8s uses these objects to represent the state of your cluster.
* Objects help in describing :
	* What containerized applications are running and on which node?
	* What resources are available to the applications?
	* Policies dictating the application behavior like restart, upgrades and fault-tolerance.
* A K8s object is a record of intent - once you create the object, K8s system will constantly work to ensure that the object exists.
* By creating an object, you are telling K8s system what you want your cluster's workload to look like. This is your cluster's `desired state`.
## Objet Spec and Status
* Every Kubernetes object includes two nested object fields that govern the object’s configuration :
	* __Object Spec__
		* Provided by user.
		* Describes the desired state i.e. the characterstics that you want the object to have.
	* __Object Status__
		* Describes the actual state.
		* Supplied and updated by K8s system.
* At any given time K8s Control Plane actively manages an object's actual state to match the desired state you supplied.
## Describing a Kubernetes Object
* When you create a new object in K8s, you must provide the object spec that describes its desired state, as well as some basic information about the object like name etc.
* To create objects you can use
	* K8s API
		* API request includes the description as JSON in request body.
	* `kubectl`
		* Description is given as YAML.
		* It is converted to JSON format when making API request.
## Required Fields
* `apiVersion` - Version of K8s API being used.
* `kind` - What kind of object is being created?
* `metadata` - Data that helps in object identification like `name`, `UID`, optional `namespace` etc.
* `spec` - Format depends based on the object being created.
# References
* https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/
