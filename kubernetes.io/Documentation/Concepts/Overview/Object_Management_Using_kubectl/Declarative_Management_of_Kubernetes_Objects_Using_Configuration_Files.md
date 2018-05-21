* K8s objects can be created, updated and deleted by storing multiple object configuration files in a directory and using `kubectl apply` to recursively create and update those objects as needed.
* This method retains the writes made to live objects without merging the changes back into the object configuration files.
# Before you begin
* Requires a firm understanding of the K8s object definitions and configuration.
## Terms used in this document :
* _Object Configuration File / Configuration File_ : Defines the configuration for a K8s object.
* _Live Object Configuration / Live Configuration_ : Live configuration values of an object as observed by the K8s cluster. These are kept in K8s cluster storage, typically etcd.
* _Declarative Configuration Writer / Declarative Writer_ : One who updates the live objects.
# How to create objects
* Use `kubectl apply` to create all objects, except those that already exist, defined by configuration files in a specified directory.
	```
	$ kubectl apply -f <directory>
	```
* This sets the `kubectl.kubernetes.io/last-applied-configuration: '{...}'` annotation on each object.
* Annotation contains the contents of the object configuration file that was used to create the object.
* Add `-R` to recursively process the subdirectories.
* Print the live configuration using
	```
	$ kubectl get -f <file|url> -o yaml
	```
# How to update objects
* `kubectl apply` can also be used to update objects.
	* Sets the field that appear in the configuration file in the live configuration.
	* Clears the field removed from the configuration file in the live configuration.
	* Add `-R` to recursively process the subdirectories.
* `kubectl scale` updates the replica fields in the live configuration.
	```
	$ kubectl scale <deployment> --replicas=<replica-count>
	```
* This sets the `kubectl.kubernetes.io/last-applied-configuration: '{...}'` annotation on each object.
* Annotation contains the contents of the object configuration file that was used to create the object.
* Print the live configuration using
	```
	$ kubectl get -f <file|url> -o yaml
	```
# How to delete objects
* Approaches :
	* __Recommended__
		* Manually deleting objects using the imperative command.
			```
			$ kubectl delete -f <filename>
			```
		* More explicit about what is being deleted.
	* __Alternative__
		* Recommened if we know what we are about the change.
			```
			$ kubectl apply -f <directory> --prune -l <labels>
			```
# How to view objects
```
$ kubectl get -f <filename|url> -o yaml
```
# How `apply` calcultaes difference and merge changes
* _Patch_
	* An update operation that is scoped to specific fields of an object instead of the entire object.
	* Enables updating specific fields on an object without reading it.
* When `kubectl apply` updates the live configuration, it does so by sending a patch request to the API server.
* The patch defines updates scoped to specific fields.
* This patch is calulated using the configuration file, live configuration and `last-applied-configuration` annotation.
## Merge Patch Calculation
1. Fields to be deleted - Fields present in `last-applied-configuration` and missing from the configuration file.
2. Fields to add or set - Fields present in the configuration file whose values don't match the live configuration. 
3. Set the `last-applied-configuration` annotation to match the value of configuration file.
4. Merge the results from 1, 2 and 3 into a single patch request to the API server.
# References
* https://kubernetes.io/docs/concepts/overview/object-management-kubectl/declarative-config/
