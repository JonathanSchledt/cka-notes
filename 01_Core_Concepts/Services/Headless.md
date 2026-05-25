# Headless Service

## Concept

Service with `clusterIP: None`

No load balancing, no cluster IP - DNS returns Pod IPs directly

Used by StatefulSets so each Pod gets a stable DNS name: `<pod-name>.<service-name>.<ns>.svc.cluster.local`

## Key Commands

```bash
k get svc

# resolve from inside a Pod
k exec -it busybox -- nslookup mysql-headless

k exec -it busybox -- nslookup mysql-0.mysql-headless
```

## Minimal YAML Example

```yaml
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
      targetPort: 3306
```
