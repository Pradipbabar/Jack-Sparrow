# Pod related objects in Kubernetes

Kubernetes provides a number of objects that can be used to manage Pods, including:

## [Pod](pod.md)

- A Pod is the smallest unit of scheduling in Kubernetes. It is a collection of one or more containers that share the same network and storage resources.
- Pods are the basic building blocks of Kubernetes. They are lightweight and ephemeral, and they are designed to be easy to create and destroy. Pods are also portable, meaning that they can be moved from one node to another without any disruption

## [Replication Controller](replication_control.md)

- A Replication Controller ensures that a specified number of Pod replicas are running at any given time.
- Replication Controllers ensure that a specified number of Pod replicas are running at any given time. This is useful for ensuring that your application is always available, even if some Pods fail.

## [ReplicaSet](replica_set.md)

- A ReplicaSet is a more advanced version of a Replication Controller that provides additional features, such as rolling updates and self-healing.
- ReplicaSet are a more advanced version of Replication Controllers that provide additional features, such as rolling updates and self-healing. Rolling updates allow you to update your Pods one at a time, without any downtime. Self-healing allows ReplicaSet to automatically create new Pods if some Pods fail.

## [Deployment](deployments.md)

- A Deployment is a higher-level concept that manages ReplicaSets and provides declarative updates to Pods along with a lot of other useful features.
- Deployments are a higher-level concept that manages ReplicaSets and provides declarative updates to Pods along with a lot of other useful features. Deployments make it easy to update your Pods without having to worry about the details.
