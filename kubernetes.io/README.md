# Features
* Production grade container orchestration.
* Automated container deployment, scaling and management.
* Groups containers that make up an application unit into logical units for easy management and discovery.
* Planet scale.
* Run anywhere on public cloud, on-premise or hybrid infrastructure.
* __Automatic Binpacking__ - Automatically places containers based on their resource requirements and other constraints, while not sacrificing availability. Mix critical and best-effort workloads in order to drive up utilization and save even more resources.
* __Horizantal Scaling__
* __Self Healing__ - Restarts containers that fail, replaces and reschedules containers when nodes die, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.
* __Service Discovery & Load Balancing__ - No need to change application. Containers have their own IP addresses and a single DNS name for a set of containers and can load balance across them.
* __Automated Rollouts & Rollbacks__ - Kubernetes progressively rolls out changes to your application or its configuration, while monitoring application health to ensure it doesn't kill all your instances at the same time. If something goes wrong, Kubernetes will rollback the change for you. Take advantage of a growing ecosystem of deployment solutions.
* __Storage Orchestration__ - Automatically mount the storage system of your choice, whether from local storage, a public cloud provider such as GCP or AWS, or a network storage system such as NFS, iSCSI, Gluster, Ceph, Cinder, or Flocker.
* __Secret & Configuration Management__ - Deploy and update secrets and application configuration without rebuilding your image and without exposing secrets in your stack configuration.
* __Batch Execution__ - In addition to services, Kubernetes can manage your batch and CI workloads, replacing containers that fail, if desired.
# References
* https://kubernetes.io/
