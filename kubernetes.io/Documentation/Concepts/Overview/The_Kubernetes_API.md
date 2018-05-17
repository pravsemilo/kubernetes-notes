* The K8s API serves as the foundation for the declarative configuration schema for the system. The `kubectl` command line can be used to create, update, delete and get API objects.
* K8s stores its serialized state (currently in `etcd`) in terms of API resources.
* K8s is decomposed into multiple components which interact through its API.
# OpenAPI and Swagger definitions
* K8s `apiserver` exposes an API that can be used to retrieve the Swagger v1.2 K8s API spec.
* This is located at `/swaggerapi`.
* Starting with K8s 1.10, OpenAPI spec is served via `/openapi/v2` endpoint.
# API versioning
* Different API versions imply different levels of stablity and support.
	* __Alpha__
		* Version name contains `alpha`.
		* May be buggy. By default these APIs are disabled.
		* Support may be dropped at any time without notice.
		* API may change in incompatible ways.
	* __Beta__
		* Version name contains `beta`.
		* Code is well tested. By default these APIs  are enabled.
		* Support for feature will not be dropped.
		* The schema or semantics of objects may change in incompatible ways in a later release.
	* __Stable__
		* Version name is `vX` where `X` is an integer.
# API groups
* API group is specified in a REST path and in the `apiVersion` field of a serialized object.
* Currently there are several API groups in use :
	* `Core`
		* Referred to as `legacy` group.
		* REST path - `/api/v1`
		* `apiVersion: v1`
	* `Named`
		* REST path - `/apis/$GROUP_NAME/$VERSION`
		* `apiVersion: $GROUP_NAME/$VERSION`
# References
* https://kubernetes.io/docs/concepts/overview/kubernetes-api/
