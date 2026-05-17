# Multi-Container Pods

## Concept

Share the same lifecycle, network, storage

Co-located Containers, Regular Init Containers, Sidecar Containers

## Minimal YAML Example

```yaml
# Co-located Containers
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp
  labels:
    name: simple-webapp
spec:
  containers:
    - name: web-app
      image: web-app
      ports:
        - containerPort: 8080
    - name: main-app
      image: main-app

# Regular Init Containers
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp
  labels:
    name: simple-webapp
spec:
  containers:
    - name: web-app
      image: web-app
      ports:
        - containerPort: 8080
  initContainers:
    - name: db-checker
      image: busybox
      command: ['wait-for-db-to-start.sh']
    - name: api-checker
      image: busybox
      command: ['wait-for-another-api.sh']

# Sidecar Containers
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp
  labels:
    name: simple-webapp
spec:
  containers:
    - name: web-app
      image: web-app
      ports:
        - containerPort: 8080
  initContainers:
    - name: log-shipper
      image: busybox
      command: ['setup-log-shipper.sh']
      restartPolicy: Always
```
