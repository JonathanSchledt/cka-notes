# Resource Requirements

## Concept
Requirements/Limits of the Pods (CPU, Memory)

LimitRange (CPU, Memory) can be set at Namespace Level

ResourceQuota (CPU, Memory) can be set at Namespace Level

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  container:
    - name: data-processor
      image: data-processor
      resources:
        requests:
          memory: "1Gi"
          cpu: 2
        limits:
          memory: "2Gi"
          cpu: 2
```
