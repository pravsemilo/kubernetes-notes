# How to create objects
* `kubectl` supports verb-driven commands for creating some of the most common object types.
	* The commands are named to be recognizable to users unfamiliar with the Kubernetes object types.
		* `run` - Create a new `Deployment` object to run `Containers` in one or more `Pods`.
		* `expose` - Create a new `Service` object to load balance traffic across `Pods`.
		* `autoscale` - Create a new `Autoscaler` object to automatically horizantally scale a controller, such as a `Deployment`.
* `kubectl` also supports creation commands driven by object type.
	* Support more object types.
	* More explicit about their intent.
	* Require users to know the type of objects they intend to create.
	```
	create <objecttype> [<subtype>] <instancename>
	```
	* Some object types have subtypes that you can specify in `create` command.
		```
		kubectl create service nodeport <myservicename>
		```
# How to update objects
* `kubectl` supports verb-driven commands for updating some of the most common object types.
	* These commands are named to enable users unfamiliar with K8s objects to perform updates without knowing the specific fields that must be set.
		* `scale` - Horizantally scale a controller to add or remove `Pods` by updating the replica count of the controller.
		* `annotate` - Add or remove a annotation from an object.
		* `label` - Add or remove a label from an object.
* `kubectl` also supports update commands driven by an aspect of the object.
	* Setting this aspect may set different fields for different object types.
		* `set` - Set an aspect for an object.
* `kubectl` supports these additional ways to update a live object directly. However they need a better understanding of the K8s object schema.
	* `edit` - Directly edit the raw configuration of a live object.
	* `patch` - Directly modify specific fields of a live object.
# How to delete objects
* You can use the `delete` command to delete an object from a cluster.
```
delete <type>/<name>
```
# How to view an object
* `get` - Prints basic information.
* `describe` - Prints aggregated detailed information about matching objects.
* `logs` - Prints the stdout and stderr for a container running in a `Pod`.
# Using `set` commands to modify objects before creation
* Not all fields have flag to be used in creation command.
* We can use a combination of `set` and `create` to specify a value for the field.
* Pipe the output of `create` command to the `set` command and then back to the `create` command.
	* Create the configuration file and but print it to stdout as YAML.
		```
		$ kubectl create service -o yaml --dry-run
		```
	* Read the configuration from stdin and write the updated configuration to stdout as YAML.
		```
		$ kubectl set --local -f - -o yaml
		```
	* Create the object using the configuration provided in stdin.
		```
		$ kubectl create -f - 
		```
# Using `--edit` to modify objects before creation
* You can use `kubectl create --edit` to make arbitrary changes to objects before it is created.
* Create the configuration file using the `--dry-run` flag of  `kubectl create` command.
* Edit the configuration file before creating the object using `kubectl create --edit` command.
# References
* https://kubernetes.io/docs/concepts/overview/object-management-kubectl/imperative-command/
