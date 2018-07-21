* Labels are key/value pairs attached to objects.
```json
"metadata": {
	"labels": {
		"key1" : "value1",
		"key2" : "value2"
	}
}
```
* Are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users, but do not directly imply semantics to the core system.
* Can be used to organize and select subset of objects.
* Can be attached at creation time and subsequently added or modified.
* Eventually these are indexed and reverse indexed for efficient queries and watches, sorting and grouping.
* Don't put large or strctured data in labels.
# Motivation
* Enable users to map their own organizational structures onto system objects without client requiring to store these mappings.
# Syntax and character set
* Valid label keys have two segments.
	* Prefix
		* Optional
		* Must be a DNS subdomain.
		* Not longer than 253 characters in total.
		* Prefix and name are separated by a slash.
		* If prefix is omitted, key is presumed to be private to the user.
	* Name
		* Required
		* Max 63 characters
		* Start and end with alphanumeric characters with dashes, dots, underscores and alphanumeric characters in between.
* `kubernetes.io/` is reserved for core K8s components.
* Valid label values
	* Max 63 characters.
	* Start and end with alphanumeric characters with dashes, dots, underscores and alphanumeric characters in between.
	* Can be empty. 
# Label Selectors
* Labels do not provide uniqueness.
* Via a _label selector_, the client/user can identify a set of objects.
* It is the core grouping primitive in K8s.
* API currently supports two types of selectors.
	* _Equality Based_
	* _Set Based_
* A label selector can be made of multiple requirements which are comma separated.
* In case of multiple requirements, all must be satisfied.
* An empty label selector selects all objects.
* A null label selector selects no objects. It is only possible for optional selector fields.
## Equality-based requirement
* Equality or inequality-based requirements allow filtering by label keys and values.
* Matching objects must satisfy all of the specified label constraints.
* Three kinds of operators are admitted `=`, `==` and `!=`.
```bash
environment = production
tier != frontend
```
## Set-based requirement
* Allows filtering keys according to a set of values.
* Three kinds of operators are admitted `in`, `notin` and `exists`.
```
environment in (production, qa)
tier notin (frontend, backend)
partition
!partition
```
# API
## LIST and WATCH filtering
* LIST and WATCH operations may specify label selectors to filter the set of objects returned using a query parameter.
## Set references in API objects
### Service and ReplicationController
* Set of pods that a `service` targets or the population of pods that a `replicationController` should manage is defined with a label selector.
* Defined in JSON or YAML.
* Only equality based requrirements are supported.
```json
"selector": {
	"component" : "redis",
}
```
### Resource that support set-based requirements
* `Job`, `Deployment`, `Replica Set` and `Daemon Set`.
* `matchLabels` is a map of `{key,value}` pairs.
* `matchExpressions` is a map of
	* `key` - Label key.
	* `operator` - `In`, `NotIn`, `Exist` and `DoesNotExist`
	* `values` - Array of label values. Not empty in case of `In` and `NotIn`.
```json
selector:
  matchLabels:
    component: redis
  matchExpressions:
    - {key: tier, operator: In, values: [cache]}
    - {key: environment, operator: NotIn, values: [dev]}
```
# References
* https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/
