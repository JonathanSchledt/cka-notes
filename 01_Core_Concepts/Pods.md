# Pods

## Concept

Smallest unit/object in k8s

## Key Commands

```bash
k run nginx
# Common flags: --image nginx

k get pods
# Common flags: -o wide/yaml/json

k describe pod myapp-pod

k delete pod myapp-pod

k run redis --image=redis --dry-run=client -o yaml > redis.yaml

k create -f redis.yaml

# run command from inside pod
k exec -it pod-name
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
    type: front-end
spec:
  containers:
    - name: nginx-container
      image: nginx
    - name: busybox-container
      image: busybox
```
