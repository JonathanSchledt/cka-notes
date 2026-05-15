# NodePort

## Concept
Mapping a Port on the Node to a Port on the Pod

Target Port: Port on the Pod
Port: Port on the Service
NodePort: Range: 30000-32767

## Key Commands

```bash
k create -f service-definition.yaml

k get svc

k expose pod redis --port=6379 --name redis-service
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: NodePort
  ports:
    - targetPort: 80
      port: 80 #port is the only mandatory field
      nodePort: 30008
  selector:
    app: myapp
    type: front-end
```
