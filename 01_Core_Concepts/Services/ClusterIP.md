# ClusterIP

## Concept

Connects the layers of a microservice application (e.g. back-end, redis)

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
  name: back-end
spec:
  type: ClusterIP #will be assumed as ClusterIP if omitted
  ports:
    - targetPort: 80
      port: 80
  selector:
    app: myapp
    type: back-end
```
