# Overview 

Kubernetes is a distributed system that consists of two main components: the control plane and the worker nodes.

- The control plane is responsible for managing the cluster, including scheduling pods, monitoring resources, and handling events. It consists of the following components:

  - API server: The API server is the front-end for the Kubernetes control plane. It exposes a RESTful API that can be used to manage the cluster.
  - Controller manager: The controller manager is responsible for running controllers, which are responsible for ensuring that the state of the cluster matches the desired state.
  - etcd: etcd is a distributed key-value store that is used to store the cluster state.

- The worker nodes are the machines that run the pods. They consist of the following components:

  - Kubelet: The kubelet is responsible for running pods on the worker node. It communicates with the API server to get the desired state of the pod and then schedules it on the node.
  - Docker: Docker is a container runtime that is used to run the containers in the pods.
  - Network proxy: The network proxy is responsible for routing traffic between pods.

## Kubernetes Objects

Kubernetes objects are the building blocks of a Kubernetes cluster. They represent different aspects of a running application, such as pods, services, and deployments.

### Pod-related Objects

- Pod is the smallest unit of execution in Kubernetes. It is a collection of containers that are scheduled and managed together.
- ReplicationController ensures that a specified number of pods are running at all times.
- ReplicaSet is a more flexible alternative to ReplicationController. It allows you to specify a desired state for a pod, and Kubernetes will ensure that the number of pods running matches the desired state.
- Deployment is a higher-level abstraction than ReplicaSet. It provides features such as rolling updates and rollbacks.
- StatefulSet is designed for stateful applications. It ensures that pods are assigned the same identity throughout their lifecycle.
- DaemonSet ensures that a pod is running on all nodes in a cluster.
- Job is used to run a one-off task.
- CronJob is used to run a task on a recurring schedule.

### Service-related Objects

- Service exposes a pod or group of pods to the outside world.
- Endpoints defines a set of IP addresses and ports that are exposed by a service.
- Ingress is used to route traffic to pods in a cluster.

### Configuration Objects

- ConfigMap is a key-value store that can be used to store configuration data.
- Secret is a secure way to store sensitive data, such as passwords and API keys.
- ResourceQuota limits the amount of resources that a pod can consume.
- LimitRange sets limits on the amount of resources that a pod can consume.

### Storage Objects

- PersistentVolume is a piece of storage that is not tied to any specific pod.
- PersistentVolumeClaim is a request for a PersistentVolume.
- StorageClass defines the quality of service for a PersistentVolume.
- VolumeSnapshot is a snapshot of a PersistentVolume.

### Networking Objects

- NetworkPolicy controls network traffic between pods.
- ServiceAccount is used to authenticate pods to access
Kubernetes resources.

### Monitoring and Logging Objects

- PodMetrics provides metrics about pods.
- Event records events that happen in the cluster.
- HorizontalPodAutoscaler automatically scales a pod based on its CPU usage.
- CustomMetric allows you to define custom metrics for pods.

### Policy Objects

- PodSecurityPolicy defines security constraints for pods.
- PodDisruptionBudget ensures that a certain number of pods in a StatefulSet or Deployment are always running.
- NetworkPolicy controls network traffic between pods.
- ResourceQuota limits the amount of resources that a pod can consume.
- LimitRange sets limits on the amount of resources that a pod can consume.

### Stateful Application Objects

- StatefulSet is designed for stateful applications. It ensures that pods are assigned the same identity throughout their lifecycle.
- PersistentVolume is a piece of storage that is not tied to any specific pod.
- PersistentVolumeClaim is a request for a PersistentVolume.
- StorageClass defines the quality of service for a PersistentVolume.

### Batch Processing Objects

- Job is used to run a one-off task.
- CronJob is used to run a task on a recurring schedule.

### Control Plane Objects

- Node is a physical or virtual machine that is running Kubernetes.
- Namespace is a logical grouping of pods, services, and other objects.
- ClusterRole defines a set of permissions that can be granted to a user or group.
- ClusterRoleBinding binds a ClusterRole to a user or group.
- Role defines a set of permissions that can be granted to a pod.
- RoleBinding binds a Role to a pod.
- ServiceAccount is used to authenticate pods to access Kubernetes resources.
- CustomResourceDefinition is used to define custom resources.
