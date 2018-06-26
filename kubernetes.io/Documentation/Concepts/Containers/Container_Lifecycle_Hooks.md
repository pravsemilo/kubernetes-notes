# Overview
* Enable containers to be aware of events in their management lifecycle.
# Container Hooks
### __PostStart__
* Execute immediately after a container is created.
* No guarantee that the hook will execute before the container ENTRYPOINT.
* No parameters are passed.
### __PreStop__
* Immediately called before a container is terminated.
* Blocking
* It must complete before the call to delete the container can be sent.
* No parameters are passed.
## Hook handler implementations
* Containers can access a hook by implementing and registering a handler for that hook.
* There are two types of hook handlers :
	* `Exec`
		* Executes a specific command inside the cgroups and namespaces of the container.
		* Resources consumed by the command are counted against the container.
	* `HTTP`
		* Executes an HTTP request against a specific endpoint on the container.
## Hook handler execution
* When a hook is called, K8s management system executes the handler in the container.
* Hook handler are synchronous within the context of pod.
	* This means that for a `PostStart` hook, container's _ENTRYPOINT_ and hook fire asynchronously.
	* If the hook takes long time, container cannot reach a `running` state.
* The behavior is similar for `PreStop` hook.
	* If the hook hangs during execution, pod stays in `terminating` state and is killed after `terminationGracePeriodSeconds`.
* If a `PostStart` or `PreHook` fails, it kills the container.
## Hook delivery guarantees
* Intended to be atleast once. Can be called multiple times.
* Generally single deliveries are made.
* In some rare cases like restart of kubelet while handling a hook, the hook might be redelivered.
## Debugging Hook handlers
* Logs for hook handlers are not exposed in Pod events.
* If a handler fails for some reason, it broadcasts an event.
	* `FailedPostStartHook` for `PostStart`
	* `FailedPreStopHook` for `PreStop`
* You can get these events by running
```
$ kubectl describe pod <pod_name>
```
# Resources
* https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/
