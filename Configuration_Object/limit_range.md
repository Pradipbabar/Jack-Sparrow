# LimitRange

**LimitRange** is a Kubernetes configuration object that helps you set default resource requirements and limits for containers within pods. It's used to enforce resource constraints, such as CPU, memory, and storage, at the container level. LimitRange helps ensure that pods adhere to resource limits, promoting resource efficiency and preventing resource hogging.

## Examples
Let's assume we want to ensure that pods within a namespace don't consume excessive CPU and memory resources.


    apiVersion: v1
    kind: LimitRange
    metadata:
    name: resource-limits
    namespace: my-namespace
    spec:
    limits:
        - max:
            cpu: "1"           # Maximum CPU limit per container
            memory: "512Mi"    # Maximum memory limit per container
        type: Container

In this example, the LimitRange named "resource-limits" enforces that each container in the namespace is limited to using at most 1 CPU core and 512MB of memory.

<br>

Suppose you want to ensure that all containers within a specific namespace have defined resource requests and limits for CPU and memory.

1. **Create a LimitRange**:

You can create a LimitRange manually or from YAML configuration. Here's a YAML example:

```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: cpu-memory-limits
spec:
  limits:
    - type: Container
      max:
        memory: "1Gi"
        cpu: "1"
      default:
        memory: "512Mi"
        cpu: "0.5"
```

In this example:
- `limits` define the constraints for containers.
- `max` specifies the maximum allowed values for CPU and memory.
- `default` sets the default values for CPU and memory if they are not explicitly specified.

2. **Apply the LimitRange**:

Apply the LimitRange to your Kubernetes cluster:

```bash
kubectl apply -f limitrange.yaml
```

3. **Use the LimitRange in a Pod**:

The LimitRange will automatically enforce the defined constraints on the pods within the specified namespace. For example, if you create a pod without specifying CPU and memory requests and limits, the values from the LimitRange will be used.

Here's an example of a pod:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: resource-pod
spec:
  containers:
    - name: app-container
      image: my-app-image
```

In this example, the `cpu-memory-limits` LimitRange will ensure that the `app-container` has a default memory request of "512Mi" and a default CPU request of "0.5". If not specified in the pod, these values will be applied.

Remember that LimitRange primarily focuses on resource constraints like CPU and memory. For other types of limits, such as the number of objects (pods, services), you might need to use other configuration objects like ResourceQuota.
