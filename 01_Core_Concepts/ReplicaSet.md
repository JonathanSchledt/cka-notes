# Replication Set

## Concept

Replication Controller (old) -> ReplicaSet (new)
ReplicaSet needs selector

## Key Commands

```bash
k create -f replicaset-definition.yaml

k get rs

k scale --replicas=6 -f replicaset-definition.yaml
```

## Minimal YAML Example

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-replicaset
  labels:
    app: myapp
    type: frontend
spec:
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
        type: front-end
    spec:
      containers:
        - name: nginx-container
          image: nginx
  replicas: 3
  selector:
    matchLabels:
      type: front-end
```
