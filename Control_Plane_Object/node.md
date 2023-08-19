# Nodes
In Kubernetes, a **node** refers to a worker machine within a cluster that is responsible for running containerized applications. Nodes are the underlying compute resources where your containers are scheduled and executed. Each node hosts one or more pods, which are the smallest deployable units in Kubernetes.

Here are some key points to understand about nodes in Kubernetes:

1. **Components on a Node:**
   Each node runs several essential components that enable it to participate in the Kubernetes cluster:
   - **Kubelet:** The Kubelet is an agent that communicates with the control plane and ensures that containers in a pod are running and healthy.
   - **Container Runtime:** This is the software responsible for running containers, such as Docker or containerd.
   - **Kube Proxy:** Kube Proxy is responsible for network routing and load balancing for services within the cluster.
   - **Node Agent:** The node agent communicates with the control plane and manages node-level operations, such as node heartbeats and monitoring.

2. **Node Identity:**
   Each node in the cluster has a unique identifier. This identifier is used to track the node's status, available resources, and the workloads it's running.

3. **Node Capacity and Resources:**
   Nodes have a certain capacity of CPU, memory, and other resources. This capacity determines how many pods can run on the node simultaneously. The kube-scheduler assigns pods to nodes based on resource requirements.

4. **Taints and Tolerations:**
   Nodes can be "tainted" to indicate that they have certain restrictions or requirements. Pods can use "tolerations" to specify that they are willing to be scheduled on nodes with specific taints.

5. **Node Conditions:**
   Nodes have various conditions that indicate their health and status. These conditions include "Ready," "OutOfDisk," "MemoryPressure," "DiskPressure," and "NetworkUnavailable."

6. **Labels and Annotations:**
   Nodes can be labeled with metadata to help with organization and filtering. Annotations can be used to store additional information about nodes.

7. **Scaling and Capacity:**
   The number of nodes in a cluster can be scaled up or down to handle varying workloads. Adding nodes increases the available capacity for running pods.

8. **Node Auto-Provisioning:**
   Some cloud providers offer auto-scaling of nodes based on the cluster's needs. Nodes are automatically added or removed to match the desired resource utilization.

Nodes play a critical role in the Kubernetes architecture, as they provide the execution environment for your containerized applications. Kubernetes manages the scheduling, placement, health, and scaling of pods across nodes to ensure the reliable and efficient operation of your workloads.