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
# References
* https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/
