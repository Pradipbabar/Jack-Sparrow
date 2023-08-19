# Resource Quota
A Resource Quota is used to limit resource consumption within a Kubernetes namespace. This helps prevent resource contention and ensures fair distribution of resources among different applications.

It is a Kubernetes configuration object that allows you to set limits on resource consumption within a specific namespace. It ensures that the total resource usage of all objects in that namespace does not exceed the defined limits. Resource Quotas help prevent one application from consuming all available resources, which could lead to performance issues or disruptions for other applications within the same namespace

## Examples
Let's say we have a namespace named "my-namespace" and we want to limit the CPU and memory resources consumed by the pods within this namespace.

```yaml
    
    apiVersion: v1
    kind: ResourceQuota
    metadata:
    name: cpu-memory-quota
    namespace: my-namespace
    spec:
    hard:
        pods: "10"              # Maximum number of pods
        requests.cpu: "2"       # Total CPU requests
        limits.cpu: "4"         # Total CPU limits
        requests.memory: "4Gi"  # Total memory requests
        limits.memory: "8Gi"    # Total memory limits
```        

In this example, the Resource Quota restricts the namespace to a maximum of 10 pods, with a total of 2 CPU cores requested and 4 CPU cores as the limit. It also enforces memory requests of up to 4GB and memory limits of up to 8GB.


<br>

Let's say you have a namespace called `my-namespace`, and you want to restrict the CPU and memory consumption of all pods, services, and replication controllers within this namespace.

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: my-resource-quota
  namespace: my-namespace
spec:
  hard:
    requests.cpu: "1"
    requests.memory: 1Gi
    limits.cpu: "2"
    limits.memory: 2Gi
```


- `requests.cpu` and `requests.memory` define the minimum required CPU and memory for each pod, service, and replication controller in the namespace.
- `limits.cpu` and `limits.memory` set the maximum allowed CPU and memory for each resource in the namespace.

For instance, with the above configuration, any pod, service, or replication controller in the `my-namespace` namespace must have at least 1 CPU unit and 1GB of memory as requested resources. Additionally, their resource usage cannot exceed 2 CPU units and 2GB of memory.

If a pod's configuration exceeds these limits, Kubernetes will prevent it from being scheduled or will throttle its resource usage, depending on the configuration and Kubernetes version.

Remember that Resource Quotas are specific to namespaces. If you have multiple namespaces, you can define Resource Quotas independently for each one to ensure resource isolation and management.

It's essential to keep in mind that Resource Quotas primarily focus on compute resources (CPU and memory) and don't cover other aspects like storage or object counts. For those, you might want to consider using other Kubernetes configuration objects like LimitRanges, PersistentVolumeClaims, or PodDisruptionBudgets.

