# Updating Images
* `IfNotPresent`
	* Default pull policy.
	* Causes kubelet to skip pulling an image if it already exists.
	* To always pull an image you can do one of the following :
		* Set the `imagePullPolicy` to `Always`.
		* Use `latest` tag for image.
		* Enable the `AlwaysPullImages` admission controller.
* If image tag is not specified, it is assumed to be `latest`.
* As a best practice, avoid using `latest` tag.
# Using a Private Registry
* May require keys to read from them.
## Using Google Container Registry
* Per-cluster
* Automatically configured on GCE or GKE.
* K8s has native support for GCR when running on GCE.
* All pods can read the project's private registry.
* All pods in the cluster have read access to images in the registry.
* kubelet will authenticate to GCR using the instance's Google service account.
* Service account on the instance has pull access but not push access.
## AWS EC2 ECR
* K8s has native support for ECR when running on EC2.
* Simply use full image name in Pod defintion.
* Use IAM roles and policies to control access to ECR repositories.
* Automatically refreshes ECR login credentials.
## Configuring nodes to authenticate to a private registry
* All pods can read any configured private registries.
* Requires node configuration by cluster administrator.
## Pre-pulling Images
* All pods can use any images cached on the node.
* Requires root access to all nodes to setup.
## Specifying ImagePullSecrets on a Pod
## Use Cases
1. Cluster running non-proprietary / open source images.
	* No need to hide images.
	* Can use public images from a public repository.
	* No other configuration.
2. Cluster running proprietary images which should be hidden to those outside the company, but visible to cluster users.
	* Use a hosted private docker registry.
		* Need to configure ~/.docker/config.json on each node.
	* Run an internal private registry with open access.
		* No other configuration.
	* On a cluster where node configuration cannot be changed, use `imagePullSecrets`.
3. Cluster with proprietary images, a few of which require stricter access control.
	* Ensure `AlwaysPullImages admission controller` is active. Otherwise all pods have access to all images.
	* Move sensitive data to `Secret` resource instead of packaging into an image.
4. A multi-tenant cluster where each tenant needs own private registry.
	* Ensure `AlwaysPullImages admission controller` is active. Otherwise all pods have access to all images.
	* Run a private registry with authorization enabled.
	* Generate registry credential for each tenant, put into secret and populate secret to each tenant namespace.
	* The tenant adds that secret to imagePullSecrets of each namespace.
# Resources
* https://kubernetes.io/docs/concepts/containers/images/
