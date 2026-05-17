# Vertical Pod Autoscaler

## Concept

Observes metrics, Adds pod resources, Balances thresholds

must be deployed (kubectl apply -f https://github.com/kubernetes/autoscaler/releases/latest/download/vertical-pod-autoscaler.yaml)

VPA Admission Controller, VPA Updater, VPA Recommender

Modes:

- Off -> Only recommends; does not change anything

- Initial -> Only changes on Pod creation; not later

- Recreate -> Evicts pods if usuage goes beyond range

- Auto -> Updates existing pods to recommended numbers - For now, it behaves like Recreate. When support for "In-Place Update of Pod Resources" is available, this mode will be preferred

## Key Commands

```bash
k get pods -n kube-system | grep vpa
```

## Minimal YAML Example

```yaml
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
  name: my-app-vpa
spec:
  targetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app
  updatePolicy:
    updateMode: "Auto"
  resourcePolicy:
    containerPolicies:
      - containerName: "my-app"
        minAllowed:
          cpu: "250m"
        maxAllowed:
          cpu: "2"
        controlledResources: ["cpu"]
```
