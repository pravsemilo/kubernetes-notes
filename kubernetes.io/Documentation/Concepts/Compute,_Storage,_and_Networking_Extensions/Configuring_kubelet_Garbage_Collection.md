* Garbage Collection
	* Function of kubelet.
	* Clean up unused images and containers.
	* Garbage collection for containers runs every minute.
	* Garbage collection for images runs every five minutes.
# Image Collection
	* Image lifecycle is managed by imageManager, with help of cadvisor.
	* Factors into consideration :
		* `HighThresholdPercent` 
		* `LowThresholdPercent`
	* Disk usage above the high threshold will trigger garbage collection.
	* Delete least recently used images until the low threshold has been met.
# Container Collection
* Considers three user-defined variables :
	* `MinAge` - Minimum age at which a container can be garbage collected.
	* `MaxPerPodContainer` - Maximum number of dead containers every single pod (UID, container name) pair is allowed to have.
	* `MaxContainers` - Maximum number of total dead containers.
* These variables can be individually disabled by :
	* `MinAge` - Set to zero. 
	* `MaxPerPodContainer` - Set to less than zero. 
	* `MaxContainers` - Set to less than zero.
* Kubelet will act on containers that are unidentified, deleted or outside of the boundaries set by the above mentioned flags.
* The oldest containers will generally be removed first. 
# References
* https://kubernetes.io/docs/concepts/cluster-administration/kubelet-garbage-collection/
