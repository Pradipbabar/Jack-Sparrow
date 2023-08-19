# Control Plane Object

1. [**Cluster:**](cluster.md)
   A Kubernetes cluster is a collection of nodes that work together to run containerized applications. It includes both control plane components (master) and worker nodes. The cluster manages the scheduling and execution of containers across nodes.

2. [**Nodes:**](node.md)
   Nodes are the worker machines that run containerized applications. They host pods, which are the smallest deployable units in Kubernetes. Each node contains runtime environments like Docker or containerd to run containers.

3. [**Roles and RoleBindings:**](roles.md)
   Roles and RoleBindings are part of Kubernetes RBAC (Role-Based Access Control) system. Roles define a set of permissions for resources within a namespace, while RoleBindings bind roles to specific users, groups, or service accounts within the same namespace. They are used to control who can access and modify resources.

4. [**Custom Resources:**](custom_resource_defination.md)
   Custom Resources allow you to extend the Kubernetes API and create your own object types. They enable you to define and manage resources specific to your application or infrastructure. Custom Resources are defined using Custom Resource Definitions (CRDs).
