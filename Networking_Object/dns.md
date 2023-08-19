In Kubernetes, DNS (Domain Name System) is an integral part of service discovery, allowing pods and services to communicate using human-readable names instead of IP addresses. DNS-related objects and configurations ensure proper name resolution within the cluster. Here are key DNS-related concepts with a brief explanation and example:

1. **Cluster DNS:**
   Kubernetes sets up a cluster-wide DNS service that provides name resolution for services, pods, and external domains. Each pod in the cluster can reach services by their service name.

2. **Service DNS:**
   Services in Kubernetes are assigned DNS names automatically based on their names and namespaces. The DNS format for a service is `<service-name>.<namespace>.svc.cluster.local`.

3. **ExternalName Service:**
   An ExternalName service allows you to map a service to an external DNS name. This is useful when you want to expose a service using an existing DNS name instead of an IP or service name.

   Example ExternalName Service:
   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: my-external-service
   spec:
     type: ExternalName
     externalName: example.com
   ```

4. **Pod DNS Policy:**
   The Pod DNS policy determines how DNS names are resolved within pods. There are two options: "ClusterFirst" (default) uses cluster DNS for internal names and falls back to external DNS, while "Default" uses the host's DNS.

5. **DNS Config:**
   You can customize DNS configuration for pods using the `dnsConfig` field. This includes setting custom DNS servers, search domains, and options.

   Example Pod with Custom DNS Config:
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: my-pod
   spec:
     dnsConfig:
       nameservers:
         - 8.8.8.8
       searches:
         - my-namespace.svc.cluster.local
     containers:
     - name: my-container
       image: nginx
   ```

These DNS-related objects and configurations ensure that communication between services and pods within a Kubernetes cluster is simplified using DNS names. DNS resolution helps in managing the dynamic nature of pods and services, enabling seamless service discovery and communication.