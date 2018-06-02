# What are controller manager metrics
* Include common Go language runtime metrics.
* Include controller specific metrics like etcd request latencies or Cloudprovider API latencies.
# Configuration
* In a cluster metrics are available from `http://localhost:10252/metrics` from the host where the controller manager is running.
* Metrics are emitted in `prometheus` format.
* Metrics are human readable.
* In a production environment, you may want to configure prometheus or some other metrics scraper to gather these metrics and make them available in a time series database.
# References
* https://kubernetes.io/docs/concepts/cluster-administration/kubelet-garbage-collection/
