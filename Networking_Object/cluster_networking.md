# Cluster Networking

Networking is a central part of Kubernetes, but it can be challenging to understand exactly how it is expected to
work. There are 4 distinct networking problems to address

- Highly-coupled container-to-container communications: this is solved by Pods and localhost communications.
- Pod-to-Pod communications.
- Pod-to-Service communications.
- External-to-Service communications.

### Container to container communication inside pod Example

```yaml
    kind: Pod
    apiVersion: v1
    metadata:
        name: testpod
    spec:
        containers:
        - name: c00
          image: ubuntu
          command: ["/bin/bash", "-c", "while true; do echo Hello-sagar; sleep 5 ; 
    done"]
        - name: c01
          image: httpd
          ports:
            - containerPort: 80
```

**Commands:**

- Kubectl apply -f filename.yaml
- kubectl logs -f testpod -c c00
- kubectl exec -it testpod -c c00 /bin/bash
- Apt update && apt install curl
- Curl localhost:80
- Now it will show the output of application which is running inside 2nd containers

### Pod to Pod Communication within same node Example:

```yaml
kind: Pod
apiVersion: v1
metadata:
    name: testpod1
spec:
    containers:
        - name: c00
          image: ubuntu
          command: ["/bin/bash", "-c", "while true; do echo Hello-sagar; sleep 5 ; done"]

---
kind: Pod
apiVersion: v1
metadata:
    name: testpod2
spec:
    containers:
        - name: c01
          image: httpd
          ports:
            - containerPort: 80
```

- Pod to communication will happen via the Ips.
- By default pod Ip will not accessible outside the node.

