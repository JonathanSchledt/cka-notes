# Probes

## Concept

Kubelet checks container health

Types:

- livenessProbe: Restart container if it fails
- readinessProbe: Remove Pod from Service endpoints if it fails (no restart)
- startupProbe: Disables liveness/readiness until it succeeds (for slow-starting apps)

Probe Handlers:

- httpGet
- tcpSocket
- exec
- grpc

Fields: initialDelaySeconds, periodSeconds, timeoutSeconds, failureThreshold, successThreshold

## Key Commands

```bash
k describe pod myapp-pod | grep -A5 -i probe

# events show probe failures
k get events --sort-by=.lastTimestamp
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
    - name: myapp
      image: myapp
      ports:
        - containerPort: 8080
      livenessProbe:
        httpGet:
          path: /healthz
          port: 8080
        initialDelaySeconds: 10
        periodSeconds: 10
        failureThreshold: 3
      readinessProbe:
        httpGet:
          path: /ready
          port: 8080
        initialDelaySeconds: 5
        periodSeconds: 5
      startupProbe:
        httpGet:
          path: /healthz
          port: 8080
        failureThreshold: 30
        periodSeconds: 10
      # tcpSocket
      # livenessProbe:
      #   tcpSocket:
      #     port: 3306
      # exec
      # livenessProbe:
      #   exec:
      #     command: ["cat", "/tmp/healthy"]
```
