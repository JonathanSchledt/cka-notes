# Horizontal Pod Autoscaler

## Concept

Observes Metrics, Adds Pods, Balances thresholds, Tracks multiple metrics

Relies on Metrics Server

## Key Commands

```bash
# manual scaling
k scale deployment my-app --replicas=3

k autoscale deployment my-app --cpu-percent=50 --min=1 --max=10

k get hpa
```

## Minimal YAML Example

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: my-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app
  minReplicas: 1
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 50
```
