# Fundamental Of Kubernetes Object Pod

- A Pod (as in a pod of whales or pea pod) is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers.
- When a Pod creation happen then master will automatically decide that on which node it should create until you have not specified the node.
- Pods remain on node until is not terminated or until node failure not happen , until pod is not deleted, lack
of required resource of pod creation

- If node die then after a timeout period pod will also get delete
- If a pod get deleted then same pod (id) cannot restart always start a new pod with different unique ID
- Volume inside pod also die if the pods die
- Controller can manage pod autoscaling, self-healing etc.

## Example OF Pod Yaml File

    apiVersion: v1
    kind: Pod
    metadata:
    name: singlecontainerpod
    spec:
    containers:
    - name: container1
    image: ubuntu
    command: ["/bin/bash", "-c", "while true; do echo c1; sleep 5 ; done"]

## Pod Example with annotation

    apiVersion: v1
    kind: Pod
    metadata:
    name: nginx
    annotations:
    description: this is demo of annotation
    spec:
    containers:
    - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80

## Pod Example with multiple containers

    apiVersion: v1
    kind: Pod
    metadata:
    name: nginx
    spec:
    containers:
    - name: container1
    image: ubuntu
    command: ["/bin/bash", "-c", "while true; do echo c1; sleep 5 ; done"]
    - name: container2
    image: ubuntu
    command: ["/bin/bash", "-c", "while true; do echo c2; sleep 5 ; done"]

## Pod Example with environment variable

    apiVersion: v1
    kind: Pod
    metadata:
    name: nginx
    spec:
    containers:
    - name: container1
    image: ubuntu
    command: ["/bin/bash", "-c", "while true; do echo c1; sleep 5 ; done"]
    env:
    - name: myname
    value: sagar

#### Ceate a pod from yaml file

Command: `Kubectl create -f filename.yaml`

#### Update a pod from yaml file

Command: `Kubectl apply -f filename.yaml`

### Those are two different approaches

1. Imperative Management
kubectl create is what we call Imperative Management. On this approach you tell the Kubernetes API what
you want to create, replace or delete, not how you want your K8s cluster world to look like.
2. Declarative Management
kubectl apply is part of the Declarative Management approach, where changes that you may have applied
to a live object (i.e. through scale) are "maintained" even if you apply other changes to the object.

#### Delete a pod from yaml file

Command: `Kubectl delete -f filename.yaml`

#### List all pods in the default namespace

Command: `Kubectl get pods`

#### List all pods in the specific namespace

Command: `Kubectl get pods-n namespace_name`

#### List all pods in the current namespace, with more details

Command: `kubectl get pods -o wide`

#### Get Pods full Information with events

Command: `kubectl describe pods pod_name`

#### Show log Of a running Pod

    kubectl logs my-pod #dump pod logs (stdout)
    kubectl logs -l name=myLabel # dump pod logs, with label name=myLabel (stdout)
    kubectl logs my-pod -c my-container # dump pod container logs (stdout, multi-container case)
    kubectl logs -l name=myLabel -c my-container # dump pod logs, with label name=myLabel (stdout)
    kubectl logs -f my-pod # stream pod logs (stdout)
    kubectl logs -f my-pod -c my-container # stream pod container logs (stdout, multi-container case)
    kubectl logs -f -l name=myLabel --all-containers # stream all pods logs with label name=myLabel (stdout)
    kubectl logs my-pod --previous # dump pod logs (stdout) for a previous instantiation of a container
    kubectl logs my-pod -c my-container --previous # dump pod container logs (stdout, multi-container case) 
    for a previous instantiation of a container
U
