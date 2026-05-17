# Secrets

## Concept

1. Create Secret

2. Inject Secret in Pod

Can also be done directly in Pod or as Volume

## Key Commands

```bash
# imperative
k create secret generic <secret-name> --from-literal=<key>=<value>

# declarative
k apply -f secret.yaml

k get secrets

echo -n 'password123' | base64 #encode

echo -n 'bXlzcWw=' | base64 --decode # decodes to mysql
```

## Minimal YAML Example

```yaml
# pod-definition.yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp-color
  labels:
    name: simple-webapp-color
spec:
  containers:
    - name: simple-webapp-color
      image: simple-webapp-color
      ports:
        - containerPort: 8080
      envFrom:
        - secretRef:
            name: app-secret

# secret-data.yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
data:
  DB_Host: bXlzcWw=
  DB_User: cm9vdA==
  DB_Password: cGFzd3Jk
```
