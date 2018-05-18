* K8s supports multiple virtual clusters backed by the same physical cluster.
* These virtual clusters are called `namespaces`.
# When to Use Multiple Namespaces
* Intended for use in environments with multiple users spread across many teams or projects.
* Namespaces provide a scope for names.
* Names of resources need to be unique within a namespace.
* Also provide a way to divide cluster resources between multiple users (via `resource quota`).
# Working with Namespaces
* K8s starts with three initial namespaces.
	* `default`
		* Default namespace for objects with no other namespace.
	* `kube-system`
		* Namespace for objects created by the K8s system.
	* `kube-public`
		* Created automatically and readable by all users (including those not authenticated). 
		* Reserved for cluster usage, in case that some resources should be visible and readable publicly throughout the whole cluster.
## Viewing namespaces
```
$ kubectl get namespaces
```
## Setting the namespace for a request
* Use the `--namespace` flag.
```
$ kubectl --namespace=your-namespace get pods
```
## Setting the namespace preference
```
$ kubectl config set-context $(kubectl config current-context) --namespace=your-namespace
$ kubectl config view | grep namespace
```
# Namespace and DNS
* When you create a `Service`, it creates a corresponding `DNS entry`.
* This entry is of the form `<service-name>.<namespace-name>.svc.cluster.local`.
* This means that if a container just uses `<service-name>`, it will resolve to the service which is local to the namespace.
* To reach across namespaces, you need to use the fully qualified domain name (FQDN).
# Not all objects are in a Namespace
* Most K8s resources (Example - pods, services, replication controller etc) are in a namespace.
* However namespace resources are not themselves in a namespace.
* Low-level resources like `nodes` and `persistentVolmes` are not in any namespace.
# References
* https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
