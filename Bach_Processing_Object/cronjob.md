# CronJobs in Kubernetes

CronJobs are a way to run one or more Pods on a repeating schedule. They are often used to run tasks that need to be performed on a regular basis, such as backups, report generation, and so on.

## Example

The following is an example of a Kubernetes CronJob that runs a Pod that prints "Hello, world!" to the console every minute:

    apiVersion: batch/v1beta1
    kind: CronJob
    metadata:
        name: hello-world
    spec:
        schedule: "*/1 * * * *"
        jobTemplate:
        spec:
            template:
                metadata:
                    name: hello-world
                spec:
                    containers:
                    - name: hello-world
                      image: busybox
                      command: ["/bin/echo", "Hello, world!"]
    restartPolicy: Never

To create this CronJob, you can use the following command:

`kubectl create -f hello-world.yaml`

This command will create a CronJob named hello-world.
 The CronJob will run a Pod every minute that prints "Hello, world!" to the console. The Pod will be restarted if it fails, but it will only be restarted a maximum of 5 times. If the Pod fails 5 times, the CronJob will be considered to have failed.

### Command

To get more information about CronJobs, you can use the following command:

`kubectl get cronjobs`

This command will list all of the CronJobs in your Kubernetes cluster. You can also use the following command to get more information about a specific CronJob:

`kubectl get cronjob hello-world`

This command will get information about the CronJob named hello-world.

Here are some additional commands that you may find useful:

To get the logs for a specific CronJob, use the following command:

`kubectl logs cronjob/hello-world`

To delete a CronJob, use the following command:

`kubectl delete cronjob hello-world`
