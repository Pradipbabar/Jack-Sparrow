# Repication Control

- Kubernetes was designed to orchestration multiple container and replication

- With the help of multiple container we can get following things
  - Reliability :
By having multiple version of an application, you prevent problem by one or more fails
  - Load Balancing:
By having multiple container of an application, enable you to easily send traffic to diff-2 instance to
prevent overloading of a single instance or node
  - Scaling:
When load become too much for existing instance then k8s enable you to easily up your application
with additional resources. And when load decrease then scale down is also possible.
  - Rolling Update:
    Update to a service by replacing pods one by one.

## Replication controller

- If there are too many pods, the Replication Controller terminates the extra pods. If there are too few, the
Replication Controller starts more pods

- A relocation controller is an object that enable you to easily create multiple pods, then make sure that
number of pods always exists.

- if a pod get crashed, terminated then RC will automatically recreate the new pod with similar
configuration.

- RC is recommended if you just want to make sure 1 pod is always running, even after system reboot.
- You can run the RC with 1 replica & the RC make sure that pod is always running.

### Example
```yaml
    apiVersion: v1
    kind: ReplicationController
    metadata:
        name: rcpod
    spec:
        replicas: 3
        selector:
            app: rcpod
        template:
            metadata:
            name: rcpod
            labels:
                app: rcpod
            spec:
                containers:
                - name: rcpod
                  image: ubuntu
                  command: ["/bin/bash", "-c", "while true; do echo c1; sleep 5 ; done"]
```

Interactive method to scaleup and scale down number of pods from RC

Command: `kubectl scale --replicas=8 rc -l app=rcpod`
