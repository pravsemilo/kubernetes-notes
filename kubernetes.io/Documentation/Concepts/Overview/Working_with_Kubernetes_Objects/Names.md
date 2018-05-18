* All objects in K8s REST API are uniquely identified by a `Name` and a `UID`.
* For non-unique user-provided attributes use `labels` and `annotations`.
# Names
* A client-provided string that refers to an object in a resource URL. Example :
```
/api/v1/pod/some-name
```
* Only one object of a given kind can have a given name at a time.
* Max length is 253 characters by convention.
* Consist of lower case alphanumeric characters, `-` and `.`.
* Certain resources have more specific restrictions.
# UIDs
* A K8s system generated string to uniquely identify objects.
* Every object created over the whole lifetime of K8s cluster has a distinct UID.
* Intended to distinguish between historical occurrences of similar entities.
# References
* https://kubernetes.io/docs/concepts/overview/working-with-objects/names/
