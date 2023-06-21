## Below Prometheus queries are for rancher Grafana.

## list namespaces and pods insdied it
```
sum by(namespace)(kube_pod_info)
```
## Number of containers by cluster and namespace without CPU limits
```
count by (namespace)(sum by (namespace,pod,container)(kube_pod_container_info{container!=""}) unless sum by (namespace,pod,container)(kube_pod_container_resource_limits{resource="cpu"}))
```
## Pod restarts by namespace
```
sum by (namespace)(changes(kube_pod_status_ready{condition="true"}[5m]))
```
## Pods not ready
```
sum by (namespace) (kube_pod_status_ready{condition="false"})
```
## CPU overcommit
```
sum(kube_pod_container_resource_limits{resource="cpu"}) - sum(kube_node_status_capacity_cpu_cores)
```
## Memory overcommit
```
sum(kube_pod_container_resource_limits{resource="memory"}) - sum(kube_node_status_capacity_memory_bytes)
```
## Number of ready nodes per cluster
```
sum(kube_node_status_condition{condition="Ready", status="true"}==1)
```
## Nodes readiness flapping
```
sum(changes(kube_node_status_condition{status="true",condition="Ready"}[15m])) by (node) > 2
```
## CPU idle by cluster
```
sum((rate(container_cpu_usage_seconds_total{container!="POD",container!=""}[30m]) - on (namespace,pod,container) group_left avg by (namespace,pod,container)(kube_pod_container_resource_requests{resource="cpu"})) * -1 >0)
```
## Memory idle by cluster
```
sum((container_memory_usage_bytes{container!="POD",container!=""} - on (namespace,pod,container) avg by (namespace,pod,container)(kube_pod_container_resource_requests{resource="memory"})) * -1 >0 ) / (1024*1024*1024)
```








