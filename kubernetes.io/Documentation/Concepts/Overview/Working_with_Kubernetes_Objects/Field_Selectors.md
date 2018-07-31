* _Field selectors_ let you select K8s resources based on value of one or more resource fields.
* They are essentialy resource filters.
* By default no selectors / filters are applied.
* Examples :
	* __metadata.name=myservice__
	* __metadata.namepsace!=default__
	* __status.phase=Pending__
# Supported fields
* Vary by K8s resource type.
* All resources support __metadata.name__ and __metadata.namespace__ fields.
# Supported operators
* `=`
* `==`
* `!=`
# Chained selectors
* Field selectors can be chained together as a comma-separated list.
# References
* https://kubernetes.io/docs/concepts/overview/working-with-objects/field-selectors/
