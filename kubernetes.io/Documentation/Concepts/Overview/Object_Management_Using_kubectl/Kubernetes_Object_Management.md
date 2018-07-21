# Management Techniques
* A Kubernetes object should be managed using only one technique. Mixing and matching techniques for the same object results in undefined behavior.

Management technique|Operates on|Recommended environment|Supported writers|Learning curve
--------------------|-----------|-----------------------|-----------------|--------------
Imperative commands|Live objects|Development projects|1+|Lowest
Imperative object configuration|Individual files|Production projects|1|Moderate
Declarative object configuration|Directories of files|Production projects|1+|Highest
# Imperative commands
* Operate directly on live objects on a cluster.
* User provides operations to the `kubectl` command as arguments or flags.
* Easy to get started.
* Better to run a one-off task in a cluster.
* No history of previous configurations.
## Examples
```bash
$ kubectl run nginx --image nginx
$ kubectl create deployment nginx --image nginx
```
## Advantages
* Commands are simple, easy to learn and remember.
* Requires a single step to make changes to cluster.
## Disadvantages
* Can't integrate with change review process.
* No audit trail associated with changes.
* No source of records except for what is live.
* No templating to create new objects.
# Imperative object configuration
* The command specifies the operation, optional flags and at least one file name.
* The file must contain a full definition of object in YAML or JSON format.
##  Examples
```bash
$ kubectl create -f nginx.yaml
$ kubectl delete -f nginx.yaml
$ kubectl replace -f nginx.yaml
```
## Advantages
* Configuration can be stored in version control system.
* Can be integrated with a change review process.
* Provides a template for creating new objects.
* Simple and easier compared to declarative configuration.
## Disadvantages
* Requires basic understanding of the object schema.
* Writing file is an additional step.
* Works best on files, not on directories.
* Updates to live objects must be reflected in configuration files. Otherwise they will be lost in the next replacement.
# Declarative object configuration
* User operates on the object configuration files stored locally.
* However user does not define the operations to be taken on the files.
* Operations are automatically detected per-object by `kubectl`.
* This enables working on directories where different operations may be needed for different objects.
## Examples
```bash
$ kubectl -f configs/
$ kubectl -f -R configs/
```
## Advantages
* Changes made directly to live objects are retained, even if they are not merged back to configuration files.
* Support to work on directories.
* Operation detection per-object.
## Disadvantages
* Debugging is harder.
* Difficult to understand the results in case of exceptions.
* Partial updates using diffs create complex merge and patch operations.
# References
* https://kubernetes.io/docs/concepts/overview/object-management-kubectl/overview/
