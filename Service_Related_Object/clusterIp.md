**ClusterIP** is a type of Kubernetes service that exposes a set of pods within the cluster. It assigns a stable IP address to the service, which is only accessible from within the cluster. This type of service is primarily used for intra-cluster communication, allowing different components within the cluster to access the service without exposing it to the external world.

Here's a brief explanation of ClusterIP with an example:

```yaml
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
kind: Deployment
apiVersion: apps/v1
metadata:
  name: ubuntudeployment
spec:
  replicas: 1
  selector: # tells the controller which pods to watch/belong to
  matchLabels:
    name: ubuntudeployment
  template:
    metadata:
      name: testpod2
      labels:
        name: ubuntudeployment
    spec:
      containers:
        - name: c01
          image: ubuntu
          command: ["/bin/bash", "-c", "while true; do echo Hello-sagar; sleep 5 ; done"]
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
    type: ClusterIP # Specifies the service type i.e ClusterIP or NodePort

```

**Example: ClusterIP Service**

Suppose you have a microservices-based application with a frontend service and a backend service. You want the frontend service to communicate with the backend service, but you don't need external access to the backend service. In this case, you can use a ClusterIP service to provide a stable internal IP address for the backend service.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: backend-service
spec:
  selector:
    app: backend
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

In this example:
- The service named `backend-service` exposes pods labeled with `app: backend`.
- It listens on port 80 and forwards traffic to the pods' port 8080.
- Since no `type` is specified, the service defaults to `ClusterIP`.

Now, any component within the Kubernetes cluster, such as the frontend service, can communicate with the backend service using the `backend-service` name and the assigned ClusterIP address. However, external traffic from outside the cluster cannot reach this service directly.

ClusterIP services are suitable for scenarios where you need to establish communication between different parts of your application within the cluster. They provide a reliable and stable internal endpoint without exposing it to the public internet.

## Commands

1. kubectl apply -f filename.yaml
2. To see all resource is running or not: kubectl get all
3. kubectl get pod -o wide 
4. Copy the httpddeployment pod IP i.e. 172.17.0.7
5. Now go inside the ubuntu pod 
6. And run apt update && apt install curl -y
7. Run "curl 172.17.0.7:80" and you will get output.
8. Run "curl clusterIP:80 i.e. curl 10.104.84.124:80 "
9. Now you hit via the pod IP and it's working 
10. But if someone delete the pod or due to any reason the pod terminated 
11. Then pod will get new IP and if you hit the command again with old pod IP then it will not give any output
12. Now we copy the Cluster Ip and again go inside the ubuntu pod
13. kubectl exec -it pod/ubuntudeployment-594f56844c-4w6sk -- /bin/bash
14. Now run "curl clusterIP:80 i.e curl 10.104.84.124:80 "
15. It will work same 
16. So now we not need to worry about POD IP.
