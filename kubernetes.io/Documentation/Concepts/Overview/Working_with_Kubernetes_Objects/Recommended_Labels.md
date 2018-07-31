* Application
	* Metadata is organized around the concept of an _application_.
	* K8s doesn't have or enforces a formal notion of application.
	* Applications are informal and described with metadata.
	* Definition of application is loose.
* Shared labels and annotations share a common prefix : `app.kubernetes.io`.
# Labels
Key|Description|Example|Type
---|-----------|-------|----
`app.kubernetes.io/name`|The name of the application|`mysql`|string
`app.kubernetes.io/instance`|A unique name identifying the instance of the application|`wordpress-abcxyz`|string
`app.kubernetes.io/version`|The current version of the application|`5.7.21`|string
`app.kubernetes.io/component`|The component within the architecture|`database`|string
`app.kubernetes.io/part-of`|The name of the higher level application this is part of|`wordpress`|string
`app.kubernetes.io/managed-by`|The tool being used to manage the operation of the application|`helm`|string
# Applications And Instances Of Applications
* An application can be installed one or more times in a cluster and in some cases in the same namespace.
* Every instance of the application must have a unique name.
# References
* https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/
