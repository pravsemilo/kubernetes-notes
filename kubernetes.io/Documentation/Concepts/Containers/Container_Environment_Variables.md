# Container Environment
* K8s container environment provides several important resources to the container.
	* A filesystem, which is a combination of an image and one or more volumes.
	* Information about the container itself.
	* Information about other object in the cluster.
## Container information
* `hostname` of a container is the name of the pod in which the container is running.
* Available through the `hostname` command.
* Pod name and namespace are available as environment variables.
* User defined environment variables from the pod defintion are also available to the container.
##  Cluster Information
* A list of all services that were running when a container was created is available to that container as environment variables.
* For a service name `foo` that maps to a container named `bar`, the following variables are defined.
```
FOO_SERVICE_HOST=<host where foo service is running on>
FOO_SERVICE_PORT=<port where foo service is running on>
```
* Services have dedicated IP addresses and are available to the container via DNS.
# References
* https://kubernetes.io/docs/concepts/containers/images/
