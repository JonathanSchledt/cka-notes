# Multiple Schedulers

## Concept

Cluster can schedule multiple schedulers at the same time

## Key Commands

```bash
#Viewing schedulers
k get pods --namespace=kube-system
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
    - image: nginx
      name: nginx
  schedulerName: my-custom-scheduler
```
