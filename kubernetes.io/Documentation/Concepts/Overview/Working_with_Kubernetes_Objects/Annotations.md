* Annotations are used to attach arbitrary non-identifying metadata to objects.
# Attaching metadata to objects
* You can use either labels or annotations to attach metadata to K8s objects.
* Labels can be used to select or find objects that satisfy certain conditions.
* In contrast, annotations are not used to identify and select objects.
* Metadata in annotations can be small or large, structured or unstructured, and can include characters not permitted by labels.
* Annotations like labels are key/value maps.
```json
"metadata": {
	"annotations": {
		"key1" : "value1",
		"key2" : "value2"
	}
}
```
* Examples of information that could be recorded in annotations :
	* Fields managed by declarative configuration layer. Attaching these fields as annotations distinguishes them from default values set by client or server and from auto-generated fields and fields set by auto-sizing and auto-scaling systems.
	* Build, release and image information like timestamps, release IDs, VCS branch etc.
	* Pointers to logging, monitoring, analytics or audit repositories.
	* Client library or tools that can be used for debugging purposes.
# References
* https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/
