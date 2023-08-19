# ConfigMap


**ConfigMaps** in Kubernetes are used to store configuration data in key-value pairs or as plain text. They provide a way to decouple configuration details from your application code, making it easier to manage and modify configuration without changing the application itself.

## Examples

Here's an example of how to create and use a **ConfigMap**:

Suppose you have an application that requires some configuration settings, such as API endpoints, database URLs, and other parameters. Let's create a ConfigMap to store these configuration values.

1. **Create a ConfigMap**:

You can create a ConfigMap manually or from YAML configuration. Here's a YAML example:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  api-url: https://api.example.com
  db-url: mysql://db.example.com:3306/mydb
```

In this example:
- `data` contains the key-value pairs of configuration data.

2. **Apply the ConfigMap**:

Apply the ConfigMap to your Kubernetes cluster:

```bash
kubectl apply -f configmap.yaml
```

3. **Use the ConfigMap in a Pod**:

You can use the ConfigMap within a pod by referencing it as environment variables or by mounting it as a volume.

Here's an example of using the ConfigMap as environment variables:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: app-pod
spec:
  containers:
    - name: my-app
      image: my-app-image
      env:
        - name: API_URL
          valueFrom:
            configMapKeyRef:
              name: app-config
              key: api-url
        - name: DB_URL
          valueFrom:
            configMapKeyRef:
              name: app-config
              key: db-url
```

In this example, the `env` section specifies that the `API_URL` and `DB_URL` environment variables should be sourced from the `app-config` ConfigMap.

You can also mount ConfigMaps as volumes:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: app-pod
spec:
  containers:
    - name: my-app
      image: my-app-image
      volumeMounts:
        - name: config-volume
          mountPath: /etc/config
  volumes:
    - name: config-volume
      configMap:
        name: app-config
```

This mounts the `app-config` ConfigMap as a volume at the path `/etc/config`.

ConfigMaps make it easier to manage configuration across multiple pods and containers, especially when you need to change configuration values without modifying your application's code. However, they are not suitable for storing sensitive information like passwords or API tokens. For those cases, you should use Secrets.

Remember that ConfigMaps are more suitable for non-sensitive configuration data that can be exposed within the pods. For sensitive data, Secrets are the recommended approach.

Suppose we have an application that requires environment variables for database connection settings.
```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
    name: app-config
    data:
    DB_HOST: "database.example.com"
    DB_PORT: "5432"
    DB_USER: "username"
    DB_PASSWORD: "password"
```
In this example, the ConfigMap named "app-config" stores the database connection settings as key-value pairs. This ConfigMap can be consumed by pods as environment variables, allowing the application to access the necessary configuration.

