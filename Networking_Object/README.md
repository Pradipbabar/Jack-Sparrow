
# Networking Object

1. ## [**Service Account:**](service_account.md)
   A **Service Account** is a Kubernetes object that provides an identity for processes (pods) to interact with the Kubernetes API and other resources. It allows pods to authenticate and authorize themselves when accessing other services, secrets, or resources within the cluster.


3. ## [**Ingress:**](ingress.md)
   An **Ingress** is a Kubernetes resource that manages external access to services within the cluster. It provides features like SSL termination, virtual hosting, and path-based routing for HTTP and HTTPS traffic. Ingress controllers (like NGINX Ingress or Traefik) implement the routing rules defined in Ingress resources.

3. ## [**NetworkPolicy:**](network_policy.md)
   A **NetworkPolicy** is a Kubernetes resource that defines rules for network access and communication between pods. It allows you to enforce security policies and control which pods can communicate with each other. NetworkPolicies work by selecting pods based on labels and applying rules to them.


4. ## [**CoreDNS:**](dns.md)
   **CoreDNS** is a flexible DNS server that is commonly used in Kubernetes clusters. It replaces kube-dns and provides DNS resolution for services, pods, and external domains. CoreDNS can be customized and extended through plugins to support various use cases.

These network-related objects and components play a crucial role in Kubernetes to ensure effective communication, security, and routing within the cluster. They allow applications to discover and interact with other services and pods while enforcing policies to maintain network segmentation and control access.