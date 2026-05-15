# ReplicationController

## Concept
Replication Controller (old) -> ReplicaSet (new)

## Key Commands

```bash
k create -f rc-definition.yaml

k get replicationcontroller
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: myapp-rc
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
```
