# Monitoring

Let's say we have a microservices application that consists of several pods serving HTTP requests. We want to monitor the health and performance of these pods and automatically scale them based on CPU utilization. We also want to set up alerts for specific conditions.

Here's how we can achieve this using the mentioned monitoring objects:

1. **Pod Metrics and Health Checks:**

We have a microservice named "web-app" running in a pod. We set up health probes to ensure the pod's health.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: web-app-pod
spec:
  containers:
    - name: web-app
      image: web-app-image
      ports:
        - containerPort: 80
      readinessProbe:
        httpGet:
          path: /health
          port: 80
        initialDelaySeconds: 5
        periodSeconds: 10
      livenessProbe:
        httpGet:
          path: /health
          port: 80
        initialDelaySeconds: 15
        periodSeconds: 20
```

In this example, the pod exposes an HTTP health endpoint at `/health`. The readiness probe checks every 10 seconds if the app is ready, and the liveness probe checks every 20 seconds if it's alive.

2. **Horizontal Pod Autoscaler (HPA):**

We want to automatically scale the "web-app" pods based on CPU utilization.

```yaml
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: web-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: web-app-deployment
  minReplicas: 2
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 50
```

In this example, the HPA scales the deployment named "web-app-deployment" based on CPU utilization. It maintains CPU utilization around 50%.

3. **Prometheus Operator:**

We deploy the Prometheus Operator and define a ServiceMonitor for our "web-app."

```yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: web-app-monitor
  namespace: default
spec:
  selector:
    matchLabels:
      app: web-app
  endpoints:
    - port: http
```

In this example, the ServiceMonitor selects pods labeled with `app: web-app` and scrapes metrics from the `/metrics` endpoint on port 80.

4. **Alertmanager:**

We define an alerting rule for when CPU utilization exceeds 80%.

```yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
  name: high-cpu-alert
  namespace: default
spec:
  groups:
    - name: HighCpuAlert
      rules:
        - alert: HighCpuUsage
          expr: sum(rate(container_cpu_usage_seconds_total{namespace="default", container="web-app"}[5m])) > 0.8
          for: 5m
          labels:
            severity: critical
          annotations:
            summary: "High CPU Usage Detected"
            description: "CPU usage on web-app exceeds 80%"
```

In this example, the PrometheusRule defines an alert that triggers when the CPU usage of the "web-app" container exceeds 80% for at least 5 minutes. The Alertmanager would handle the alert and notify relevant parties.
