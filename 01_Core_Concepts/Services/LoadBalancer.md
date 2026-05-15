# LoadBalancer

## Concept
Usually supplied by Cloud Provider, if not provided same effect as setting to NodePort

## Key Commands

```bash
k create -f service-definition.yaml

k get svc
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: LoadBalancer
  ports:
    - targetPort: 80
      port: 80 #port is the only mandatory field
      nodePort: 30008
  selector:
    app: myapp
    type: front-end
```
