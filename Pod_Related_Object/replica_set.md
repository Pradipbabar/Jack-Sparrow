# ReplicaSets

- ReplicaSets is a next generation Replica Controller
- The replica controller only supports equality based selector but replica sets supports set based selector
i.e. filtering according to the set of values.

- A Replica Set's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is
often used to guarantee the availability of a specified number of identical Pods

## How a ReplicaSet works

- In replicasets there is a lot of properties which helps replicasets to work properly.
- There is selector properties which helps replicasets to recreate the pods based on label when pod failure
happen, also helped to group the same label pods.

- There is one more properties called template that help RS to create pod according to the given pod template

- Replicas properties is used to provide the number of desired pods to create

## When to use a ReplicaSet

- A ReplicaSet ensures that a specified number of pod replicas are running at any given time.

- However, a Deployment is a higher-level concept that manages ReplicaSets and provides
declarative updates to Pods along with a lot of other useful features. Therefore, we
recommend using Deployments instead of directly using ReplicaSets, unless you require
custom update orchestration or don't require updates at all.

- This actually means that you may never need to manipulate ReplicaSet objects: use a
Deployment instead, and define your application in the spec section

## Example

    apiVersion: apps/v1
    kind: ReplicaSet
    metadata:
        name: frontend
        labels:
            app: guestbook
            tier: frontend
    spec:
    # modify replicas according to your case
        replicas: 3
        selector:
            matchLabels:
                tier: frontend
        template:
            metadata:
                labels:
                    tier: frontend
            spec:
                containers:
                - name: php-redis
                  image: gcr.io/google_samples/gb-frontend:v3
