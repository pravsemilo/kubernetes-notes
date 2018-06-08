# Organizing resource configurations
* Management of multiple resources can be simplified by grouping them together in the same YAML file, separated by `---`.
* Multiple resources can be created the same way as a single resource.
```
$ kubectl create -f <file>
```
* Resources are created in the order mentioned in the file.
# Bulk operations in kubectl
# Using labels effectively
* We can display specific labels in `kubectl get` command.
# Canary deployments
* Can be acheived via label selectors.
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
