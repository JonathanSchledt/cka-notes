# Priority Classes

## Concept

Determines which Pods run if resources are sparse

## Key Commands

```bash
k get priorityclass
```

## Minimal YAML Example

```yaml
#Pod
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
    - name: nginx-container
      image: nginx
  priorityClassName: high-priority

#priority class
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: high-priority
value: 1000000000
description: "Priority class for mission critical pods"
globalDefault: true
```
