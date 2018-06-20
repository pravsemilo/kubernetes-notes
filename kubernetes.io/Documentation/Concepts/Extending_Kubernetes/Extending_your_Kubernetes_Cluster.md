* K8s is highly configurable and extensible.
# Configuration
* Involves changing flags, local configuration files or API resources.
* Flags and configuration files :
	* May not always be changable in case of hosted K8s service.
	* Changable by cluster administrator.
	* May change in future K8s versions.
	* May need restart.
	* Hence should be used when other options are not viable.
* _Built-in Policy APIs_
	* Examples : `ResourceQuota`, `PodSecurityPolicy`, `NetworkPolicy` and `RBAC`.
	* Can be used with hosted K8s service.
	* Declarative hence repeatable.
	* If they are stable, they have a support policy.
	* Hence preferred over flags and configuration files.
# Extensions
* Involve running additional programs or services.
* Extensions are software components that extend and deeply integrate with K8s.
* Help to adapt K8s to support new types and new kinds of hardware.
# Extension Patterns
* K8s is designed to be automated by writing client programs.
* _Controller Pattern_
	* Controllers read an object's `.spec`, do something and then update object's `.status`.
	* Controller is a client of K8s.
* _Webhook_
	* When K8s is the client and calls out a remote service.
	* Remote service is called _Webhook Backend_.
	* Add a point of failure.
* _Binary Plugin_
	* K8s executes a binary.
	* Used by `kubelet` and `kubectl`. Example : `Flex Volume Plugins` & `Network Plugins`.
# Extension Points
* `kubectl`
	* `kubectl plugins` extend the kubectl binary.
	* Only affect the user's local environmennt.
* `apiserver`
	* Examples include authentication, deletion, content type filtering etc.
* `Resources`
	* Built-in resource kinds can't be changed.
	* `Custom Resources`
		* Resources defined by third parties.
		* Used with `API Access Extensions`.
* `K8s Scheduler`
	* Extend scheduling using `Scheduler Extensions`.
* `Controllers`
	* Clients of API Server.
	* Used in conjunction with `Custom Resources`.
* `Network Plugins`
	* Pod networking implementations.
* `Storage Plugins`
# API Extensions
## User-Defined Types
* Consider adding a `Custom Resource` to K8s if you want to define new controllers, application configuration objects or other declarative APIs and to manage them using K8s tools like `kubectl`.
* Do not use `Custom Resource` as a data storage for application or for monitoring data.
## Combining New APIs with Automation
* When you add a new API, you also add a control loop that read and / or writes the new API.
* When a combination of new API and control loop is used to manage an application, this is called _Operator Pattern_.
## Changing Built-in Resources
* When you extend K8s API by adding custom resources, the added resources fall into new _API Groups_.
* You cannot replace or change existing groups.
* Adding an API doesn't directly let you affect the behavior of existing APIs, but _API Access Extension_ do.
## API Access Extensions
* When a request reaches K8s API Server, it is first authenticated, authorized and then subject to various _Admission Control_.
* Each of these steps offer extension points.
* K8s has support for several built-in authentication methods.
* It can also sit behind an authenticating proxy.
* It can also send an _Authentication_ header to a remote service for verification via webhook.
## Authentication
* Maps headers or certificates in all requests to a username for the client making the request.
## Authorization
* Works at the level of whole resource. Doesn't discriminate based on arbitrary object fields.
* `Authorization Webhook` allows calling to user-provided code.
## Dynamic Admission Control
* After a request is authorized, it goes through a series of `Admission Control` steps.
* In addition to several built-in steps, there are several extensions.
	* `Image Policy Webhook` : What images can be run in containers?
	* `Admission Webhook` : For arbitrary admission control decisions.
	* `Initializers` : Controllers that modify objects before they are created. Can also reject objects.
# Infrastructure Extensions
## Storage Plugins
* `Flex Volumes` : Allow users to mount volume types without built-in support by having the kubelet call a binary plugin to mount the volume.
## Device Plugins
* Allow a node to discover new Node resources.
## Network Plugins
## Scheduler Extensions
* Scheduler is a special type of controller that watches pods and assigns pods to nodes.
* Default scheduler can be replaced.
* Multiple schedulers can run at the same time.
* Also supports a webhook that permits a webhook backend to filter and prioritize the nodes chosen for a pod.
# References
* https://kubernetes.io/docs/concepts/extend-kubernetes/extend-cluster/
