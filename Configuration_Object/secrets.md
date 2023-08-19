# Secrets


**Secrets** in Kubernetes are used to securely store and manage sensitive information, such as authentication tokens, API keys, and passwords. They provide a way to ensure that sensitive data is not stored in plain text within configuration files or exposed to unauthorized users.

## Example:


Here's an example of how to create and use a **Secret**:

Suppose you have an application that requires access to a database, and you want to securely store the database credentials. Let's create a Secret to store the database username and password.

1. **Create a Secret**:

You can create a Secret manually or from YAML configuration. Here's a YAML example:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-credentials
type: Opaque
data:
  username: YWRtaW4=  # Base64 encoded "admin"
  password: cGFzc3dvcmQ=  # Base64 encoded "password"
```

In this example:
- `type: Opaque` indicates that this Secret can store arbitrary key-value pairs.
- `data` contains the actual sensitive data encoded in Base64.

To encode your data to Base64, you can use the command-line tool or any programming language/library that supports Base64 encoding.

2. **Apply the Secret**:

Apply the Secret to your Kubernetes cluster:

```bash
kubectl apply -f secret.yaml
```

3. **Use the Secret in a Pod**:

You can use the Secret within a pod by referencing it as an environment variable or by mounting it as a volume.

Here's an example of using the Secret as environment variables:

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
        - name: DB_USERNAME
          valueFrom:
            secretKeyRef:
              name: db-credentials
              key: username
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: db-credentials
              key: password
```

In this example, the `env` section specifies that the `DB_USERNAME` and `DB_PASSWORD` environment variables should be sourced from the `db-credentials` Secret.

You can also mount Secrets as volumes:

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
        - name: secret-volume
          mountPath: /etc/secret
  volumes:
    - name: secret-volume
      secret:
        secretName: db-credentials
```

This mounts the `db-credentials` Secret as a volume at the path `/etc/secret`.

Remember that Secrets are base64-encoded, not encrypted. While they provide a layer of security, they are not the best solution for highly sensitive data. For that, you might consider using external secrets management tools or encryption mechanisms.