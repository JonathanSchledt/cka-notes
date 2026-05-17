# Environment Variables and Config Maps

## Concept

1. Create ConfigMap

2. Inject into Pod

Can also be done directly in Pod or as Volume

## Key Commands

```bash
docker run -e APP_COLOR=pink simple-webapp-color

# imperative
k create configmap <config-name> --from-literal=<key>=<value>

# declarative
k apply -f config-map.yaml

k get cm
```

## Minimal YAML Example

```yaml
# env variables directy in pod
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp-color
spec:
  containers:
    - name: simple-webapp-color
      image: simple-webapp-color
      ports:
        - containerPort: 8080
      env:
        - name: APP_COLOR
          value: pink

# config-map.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_COLOR: blue
  APP_MODE: prod

# Inject config
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp-color
spec:
  containers:
  - name: simple-webapp-color
    image: simple-webapp-color
    ports:
      - containerPort: 8080
    envFrom:
      - configMapRef:
          name: app-config
```
