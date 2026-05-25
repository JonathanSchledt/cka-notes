# StatefulSets

## Concept

Like Deployment but for stateful apps (databases, queues)

Guarantees:

- Stable, ordered Pod names: `<name>-0`, `<name>-1`, ...
- Stable network identity via headless Service
- Ordered, sequential scaling and rolling updates (0 -> 1 -> 2)
- Each Pod gets its own PVC via volumeClaimTemplates

Requires a headless Service (clusterIP: None) referenced by `serviceName`

## Key Commands

```bash
k get sts

k describe sts mysql

# scale (one Pod at a time)
k scale sts mysql --replicas=5

# delete sts but keep Pods
k delete sts mysql --cascade=orphan
```

## Minimal YAML Example

```yaml
# headless service (required)
apiVersion: v1
kind: Service
metadata:
  name: mysql-headless
spec:
  clusterIP: None
  selector:
    app: mysql
  ports:
    - port: 3306

# statefulset
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql
spec:
  serviceName: mysql-headless
  replicas: 3
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
        - name: mysql
          image: mysql:8
          ports:
            - containerPort: 3306
          volumeMounts:
            - name: data
              mountPath: /var/lib/mysql
  volumeClaimTemplates:
    - metadata:
        name: data
      spec:
        accessModes: ["ReadWriteOnce"]
        resources:
          requests:
            storage: 1Gi
```
