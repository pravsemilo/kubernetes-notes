# Organizing resource configurations
* Management of multiple resources can be simplified by grouping them together in the same YAML file, separated by `---` sections in the file.
* Multiple resources can be created the same way as a single resource.
	* Resources are created in the order they appear in the file.
* `kubectl create` also accepts multiple `-f` arguments.
```
$ kubectl create -f <file1> -f <file2>
```
# Bulk operations in kubectl
* Can bulk delete by specifying resource names in file.
* Can use label selectors for bulk operations.
# Using labels effectively
* We can display specific labels in `kubectl get` command.
```
$ kubtectl get pods -L<label-name>
```
# Canary deployments
* Can be acheived via label selectors.
# Updating labels
```
$ kubectl label pods -l <existing-name>=<existing-value> <new-label>=<new-value>
```
# Updating annotations
```
$ kubectl annotate pods <pod-name> <annotation-name>=<annotation-value>
```
# Scaling your application
```
$ kubectl scale deployment/my-nginx --replicas=1
$ kubectl autoscale deployment/my-nginx --min=1 --max=3
```
# In-place update of resources
## `kubectl apply`
## `kubectl edit`
* Edit the configuration in a file before applying.
## `kubectl patch`
* Supports JSON patch, JSON merge patch and strategic merge patch.
# Resources
* https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/
