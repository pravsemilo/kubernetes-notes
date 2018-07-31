* K8s objects can be created, deleted and updated by using `kubectl` along with an object configuration file in YAML or JSON.
# How to create objects
```bash
$ kubectl create -f <filename|url>
```
# How to update objects
```bash
$ kubectl replace -f <filename|url>
```
* Updating objects with the `replace` command drops all parts of the spec not specified in the configuration file.
* This should not be used with objects whose specs are partially managed by the cluster.
* Independently managed fields must be copied to the configuration file to prevent `replace` from dropping them.
# How to delete objects
```bash
$ kubectl delete -f <filename|url>
```
# How to view an object
```bash
$ kubectl get -f <filename|url> -o yaml
```
# Limitations
* The `create`, `replace` and `delete` commands work well when each object's configuration is fully defined and recorded in it's configuration file.
* If you need to support multiple writers to the same object, you can use `kubectl apply` to manage the object.
# Creating and editing an object from a URL without saving the configuration
```bash
$ kubectl create --edit
```
# Migrating from imperative commands to imperative object configuration
* Export the live object to a local object configuration file.
	```bash
	$ kubectl get / -o yaml -export > _.yaml
	```
* Manually remove the status field from the object configuration file.
* For subsequent object management, use `replace`.
	```bash
	$ kubectl replace -f _.yaml
	```
# References
* https://kubernetes.io/docs/concepts/overview/object-management-kubectl/imperative-config/
