* K8s is a portable, extensible open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation.
# Why do I need Kubernetes and what can it do?
* K8s can be thought of as
	* Container Platform
	* Microservices Platform
	* Portable Cloud Platform
* Provides a container-centric management environment.
* Orchestrates computing, network and storage infrastructure on behalf of user workloads.
* Enables portability across infrastructures provides.
* Provides simplicity of PaaS with flexibility of IaaS.
# How is Kubernetes a platform?
* _Labels_ empower users to organize their resources however they please.
* _Annotations_ enable users to decorate resources with custom information to facilitate their workflows and provide an easy way for management tools to checkpoint state.
* Kubernetes control plane is built upon the same APIs that are available to developers and users. Users can write their own controllers, such as schedulers, with their own APIs that can be targeted by a general-purpose command-line tool.
* This design has enabled a number of other systems to build atop Kubernetes.
# What Kubernetes is not?
* K8s is not a traditional, all-inclusive PaaS.
* It provides some generally applicable features common to PaaS offerings, such as deployment, scaling, load balancing, logging, and monitoring.
* K8s provides the building blocks for building developer platforms, but preserves user choice and flexibility where it is important.
* Does not limit the types of applications supported.
* Does not deploy source code and does not build your application.
* Does not dictate logging, monitoring, or alerting solutions. It provides some integrations as proof of concept, and mechanisms to collect and export metrics.
* Does not provide application-level services, such as middleware, database, cache etc.
* Does not provide nor mandate a configuration language / system (e.g., jsonnet). It provides a declarative API that may be targeted by arbitrary forms of declarative specifications.
* Does not provide nor adopt any comprehensive machine configuration, maintenance, management or self-healing systems.
* K8s is not a mere orchestration system. In fact, it eliminates the need for orchestration.
* In contrast, K8s is comprised of a set of independent, composable control processes that continuously drive the current state towards the provided desired state.
# References
* https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/
