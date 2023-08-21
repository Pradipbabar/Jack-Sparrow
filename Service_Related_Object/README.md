
# Service

### Issue:
Each pod gets its own IP address and when we deploy the pod via deployment or ReplicaSets then it creates the 
pod with a unique IP address and we provide that IP to other users/pods/applications/frontend to use. And now 
let's suppose due to some issue pods get terminated and now RS will again create the pod with a new IP address 
then again we need to update all users/pods/applications/frontend and if it happens a lot of time so it's hard to 
remember the IP address of pods or hard to update at runtime. so solution of this issue is service object. 

In other words:

Kubernetes Pods are created and destroyed to match the desired state of your cluster. Pods are nonpermanent 

resources. If you use a Deployment to run your app, it can create and destroy Pods dynamically.

Each Pod gets its own IP address, however in a Deployment, the set of Pods running in one moment in time could 
be different from the set of Pods running that application a moment later.

This leads to a problem: if some set of Pods (call them "backends") provides functionality to other Pods (call them 
"frontends") inside your cluster, how do the frontends find out and keep track of which IP address to connect to, 
so that the frontend can use the backend part of the workload?

## Service:

- When using RC,RS,deployement, pods are terminated and created during scaling or replication operations
- When using deployment , while updating the image version the pods are terminated and new pods take the 
place of other pods.

- Pods are very dynamic i.e. they come & go on the k8s cluster and on any of the available nodes & it would 
be difficult to access the pods as the pods IP changes its recreated.

- Service objects is an logical bridge between pods and end user, which provide virtual IP
- Service allow client to reliably connect to the the containers running in the pod using the VIP
- The VIP is not a actual IP connected to a network interface, but its purpose is purely forward traffic to one or 
more pods

- kube proxy is the one which keeps the mapping between the VIP and pods up to date, which queries the API 
server to learn about new services in the cluster 

- Although each pod having unique IP address, but those are not accessible outside the cluster.
- Services help to expose the VIP mapped to the pod & allow application to receive traffic 
- Label are used to select which are the pods to be put under the service
- Creating a service will create an endpoint to access the pods/application in it.
Service can be expose in 3 different way be specifying a type in the service spec
   - Cluster IP
   - Node Port
   - Load Balancer

- By default service can run only between ports 30,000 - 32767.
- The set of pods targeted by a service usually determined by a selector

## [**ClusterIP:**](clusterIp.md)

   A **ClusterIP** service exposes a set of pods as an internal service within the Kubernetes cluster. This type assigns a stable IP address to the service that is accessible only from within the cluster. It's mainly used for intra-cluster communication, allowing various components within the cluster to access the service using the ClusterIP. External traffic from outside the cluster cannot directly reach a ClusterIP service.

   **Use Case Example:** Suppose you have a backend service that needs to be accessed by various frontend components within the same Kubernetes cluster. You'd use a ClusterIP service to provide a consistent and internal endpoint for the frontend to communicate with the backend.

## [**NodePort:**](nodeport.md)
   A **NodePort** service exposes the service on a static port on every node's IP address in the cluster. This makes the service accessible from outside the cluster by targeting any node's IP and the specified NodePort. Incoming traffic on the NodePort is then routed to the corresponding service and its pods. NodePort services provide a simple way to expose services externally without relying on external load balancers.

   **Use Case Example:** Imagine you have a web application running in your cluster. By using a NodePort service, you can allow external users to access your application using the NodePort number along with any node's IP address.

## [**LoadBalancer:**](loadbalancer.md)
   A **LoadBalancer** service is used to expose services using a cloud provider's load balancer. The cloud provider's load balancer distributes incoming traffic to the pods associated with the service. This type is particularly useful when you need to expose your services to the external world, and you want to leverage the load balancing capabilities provided by the cloud provider.

   **Use Case Example:** When running your application in a cloud environment, you can use a LoadBalancer service to ensure that incoming traffic from external users is distributed efficiently among your application's pods, enhancing availability and scalability.

In summary, ClusterIP is for internal cluster communication, NodePort is for exposing services externally via a specific port on the nodes, and LoadBalancer is for utilizing cloud provider load balancers to distribute traffic externally to your service's pods. These service types cater to different scenarios and needs, providing flexibility in how you expose and manage your applications in Kubernetes.