# NodePort

**NodePort** is a type of Kubernetes service that exposes a service on a static port on each node's IP address. This allows external traffic to reach the service by targeting any node's IP along with the specified NodePort. The request is then forwarded to the appropriate pods. NodePort services provide a simple way to expose services externally without relying on external load balancers.

1. Make your service available outside your cluster
2. Expose the service on the same port of each selected node in the cluster using NAT.
3. This is top level of service of clusterIP
4. Here only port we need to know and instead of IP we will use Public Ip of our host.
If you set the type field to NodePort, the Kubernetes control plane allocates a port from a range specified 
by --service-node-port-range flag (default: 30000-32767).
5. Each node proxies that port (the same port number on every Node) into your Service. Your Service reports 
the allocated port in its .spec.ports[*].nodePort field

6. When you only pass .spec.type to NodePort then it will take any random unique port from the default range 
7. But If you want to specify particular IP(s) to proxy the port, you can set the --nodeport-addresses flag for 
kube-proxy or the equivalent nodePortAddressesfield of the kube-proxy configuration file to particular IP 
block(s).

## Examples

```yaml

apiVersion: v1
kind: Service
metadata:
 name: my-service
spec:
 type: NodePort
 selector:
 app.kubernetes.io/name: MyApp
 ports:
 # By default and for convenience, the `targetPort` is set to the same value as the `port` field.
 - port: 80
 targetPort: 80
 # Optional field
 # By default and for convenience, the Kubernetes control plane will allocate a port from a range (default: 
30000-32767)
 nodePort: 30007


----

kind: Deployment
apiVersion: apps/v1
metadata:
  name: httpddeployment
spec:
  replicas: 1
  selector: # tells the controller which pods to watch/belong to
    matchLabels:
      name: httpddeployment
  template:
    metadata:
      name: testpod1
      labels:
        name: httpddeployment
    spec:
      containers:
        - name: c00
          image: httpd
          ports:
          - containerPort: 80
---

kind: Service # Defines to create Service type Object
apiVersion: v1
metadata:
  name: demoservice
spec:
  ports:
  - port: 80 # Containers port exposed
    targetPort: 80 # Pods port
  selector:
    name: httpddeployment # Apply this service to any pods which has the specific label
  type: NodePort # Specifies the service type i.e ClusterIP or NodePort
```

**Example: NodePort Service**

Imagine you have a web application that consists of multiple pods and you want to expose it externally on a specific port. You can use a NodePort service to achieve this.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  selector:
    app: web-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: NodePort
```

In this example:
- The service named `web-service` exposes pods labeled with `app: web-app`.
- It listens on port 80 and forwards traffic to the pods' port 8080.
- The `type` is set to `NodePort`, indicating that it's a NodePort service.

After creating this NodePort service, each node in your cluster will open the specified NodePort (e.g., 30000-32767) to route incoming traffic to the pods associated with the service. External users can then access the application by targeting any node's IP address and the NodePort number.

For instance, if you're using a NodePort of 30080, users can access the application using `http://<node-ip>:30080`.

NodePort services are often used when you want to expose applications externally without using a cloud provider's load balancer or when you're testing and developing on a local or non-cloud environment.

## Commands

1. kubectl apply -f filename.yaml
2. Kubectl get all
3. To check all resource is up and running 
4. Sometime your pod will show imagepullerror then check image path and path is correct then delete your 
pod and deployment recreate it automatically 

5. For delete pod use the following command:
kubectl delete pod/pod_name
6. And now deployment will recreate 
7. Now check the minikube public service URL of nodeport to access our pod service from outside the cluster 
for that use the below command

8. minikube service list
9. Now get the URL and hit from browser and you get the desired output
