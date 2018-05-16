# Service Catalog
* Extension API that enables applications running in K8s clusters to easily use external managed software offerings.
* Provides a way to list, provison and bind with external _Managed Services_ from _Service Brokers_.
* __Service Broker__
	* An endpoint for a set of managed services offered and maintained by a third party.
# Architecture
* Uses the _Open service broker API_ to communicate with service brokers, acting as an intermediary for the K8s API server to negotiate the initial provisioning and retrieve the credentials necessary.
* Implemented as an extension API server and controller, using etcd for storage.
* Also uses _aggregation layer_ to present its API.
## API Resources
* Service catalog installs the `servicecatalog.k8s.io` API and provides following K8s resources.
	* `ClusterServiceBroker` - An in-cluster representation of a service broker, encapsulating its server connection details. These are created and managed by cluster operators who wish to use that broker server to make new types of managed services available within their cluster.
	* `ClusterServiceClass` - A managed service offered by a particular service broker. When a new `ClusterServiceBroker` resource is added to the cluster, the Service Catalog controller connects to the service broker to obtain a list of available managed services. It then creates a new `ClusterServiceClass` resource corresponding to each managed service.
	* `ClusterServicePlan` - A specific offering of a managed service. Similar to `ClusterServiceClass`, when a new `ClusterServiceBroker` is added to the cluster, Service Catalog creates a new `ClusterServicePlan` resource corresponding to each Service Plan available for each managed service.
	* `ServiceInstance` - A provisioned instance of a `ClusterServiceClass`. These are created by cluster operators to make a specific instance of a managed service available for use by one or more in-cluster applications. When a new `ServiceInstance` resource is created, the Service Catalog controller connects to the appropriate service broker and instruct it to provision the service instance.
	* `ServiceBinding` - Access credentials to a `ServiceInstance`. These are created by cluster operators who want their applications to make use of a `ServiceInstance`. Upon creation, the Service Catalog controller creates a Kubernetes `Secret` containing connection details and credentials for the Service Instance, which can be mounted into Pods.
## Authentication
* Basic
* OAuth 2.0 Bearer Token
# Usage
## Listing managed services and Service Plans
* A cluster operator must create a `ClusterServiceBroker` resource within the `servicecatalog.k8s.io` group. This resource contains the URL and connection details necessary to access a service broker endpoint.
* Once the `ClusterServiceBroker` resource is added to Service Catalog, it triggers a call to the external service broker for a list of available services.
* The service broker returns a list of available managed services and a list of Service Plans, which are cached locally as `ClusterServiceClass` and `ClusterServicePlan` resources respectively.
* A cluster operator can then get the list of available managed services and their plans.
## Provisioning a new instance
* A cluster operator can initiate the provisioning of a new instance by creating a `ServiceInstance` resource.
* When the `ServiceInstance` resource is created, Service Catalog initiates a call to the external service broker to provision an instance of the service.
* The service broker creates a new instance of the managed service and returns an HTTP response.
* A cluster operator can then check the status of the instance to see if it is ready.
## Binding to a managed service
* After a new instance has been provisioned, a cluster operator must bind to the managed service to get the connection credentials and service account details necessary for the application to use the service.
* This is done by creating a `ServiceBinding` resource.
* After the `ServiceBinding` is created, Service Catalog makes a call to the external service broker requesting the information necessary to bind with the service instance.
* The service broker enables the application permissions / roles for the appropriate service account.
* The service broker returns the information necessary to connect and access the managed service instance. This is provider and service-specific so the information returned may differ between Service Providers and their managed services.
## Mapping the connection credentials
* After binding, the final step involves mapping the connection credentials and service-specific information into the application. These pieces of information are stored in secrets that the application in the cluster can access and use to connect directly with the managed service.
# References
* https://kubernetes.io/docs/concepts/service-catalog/
