# Namespaces

## Concept

- Logical Isolation of Resources (e.g default, kube-system, kube-public, dev, int, prod)
- Namespaces can have their own assigned policies and resources

Inside current Namespace -> Address Resources by first name: mysql.connect("db-service")
Outside current Namespace -> Address Resources by firs + last name: mysql.connect("db-service.dev.svc.cluster.local")

## Key Commands

```bash
k create -f namespace-dev.yaml

k create ns dev

#switch context
k config set-context $(k config current-context) --namespace=dev

k get pods --namespace=kube-system

k get pods --all-namespaces

k get pods -n=dev
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```
