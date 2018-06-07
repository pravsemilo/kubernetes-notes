# Organizing resource configurations
* Management of multiple resources can be simplified by grouping them together in the same YAML file, separated by `---`.
* Multiple resources can be created the same way as a single resource.
```
$ kubectl create -f <file>
```
	* Resources are created in the order mentioned in the file.
# Bulk operations in kubectl
# Resources
* https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/
