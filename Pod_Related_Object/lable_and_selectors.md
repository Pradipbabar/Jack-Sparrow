# Lable & Selectors

## Labels

- Labels are the mechanism you use to organize the Kubernetes objects
- Labels are key value paired without any predefined meaning that can be attach to objects
- Labels are similar to tag in AWS and GIT
Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to
users, but do not directly imply semantics to the core system
- Labels can be attached to objects at creation time and subsequently added and modified at any time
- You are free to choose labels as you need it to refers an environment which is used for dev or Testing or
production, refer a product group like Deployment A, Deployment B

### Valid label value

- must be 63 characters or less (can be empty),
- unless empty, must begin and end with an alphanumeric character ([a-z0-9A-Z]),
- could contain dashes (-), underscores (_), dots (.), and alphanumeric between.

- Apply label on pod via imperative method
  - Kubectl label pod{object} object_name env=dev

### Example of Declarative
```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: label-demo
        labels:
            environment: production
        app: nginx
        spec:
            containers:
            - name: nginx
              image: nginx:1.14.2
              ports:
            - containerPort: 80
```    
Command:

1. Kubectl get pods{object} --show-labels
2. Kubectl get pods{object} -l env=dev
3. Kubectl get pods{object} -l env!=dev

Note: there is 3 way to delete an object

1. From yaml file
2. Kubectl delete object object_name
3. Kubectl delete object -l env=dev

## Selectors

- Unlike names and UIDs, labels do not provide uniqueness. In general, we expect many objects to carry the
same label(s).

- Via a label selector, the client/user can identify a set of objects. The label selector is the core grouping
primitive in Kubernetes.

- The API currently supports two types of selectors
    1. equality-based (=, !=)
    2. Set-based (in, notin, exists)

### NodeSelector

- nodeSelector is the simplest recommended form of node selection constraint.
- You can add the nodeSelector field to your Pod specification and specify the node labels you want the target
node to have. Kubernetes only schedules the Pod onto nodes that have each of the labels you specify.

#### Example
```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: nginx
        spec:
            containers:
                - name: nginx
                  image: nginx
                  nodeSelector:
                    nodename: minikubenod
```