# Service Accounts

## Concept

User vs. Service Accounts

Service Account -> Identity of a Service

Tokens are created for Service Accounts to prove identity

Service Account mounted at /var/run/secrets/kubernetes.io/serviceaccount

## Key Commands

```bash
k get sa

k create sa name-sa

k create token name-sa --duration 2h (default 1 hour)
```

## Minimal YAML Example

```yaml
# service-definition.yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: dashboard-sa
  namespace: default
automountServiceAccountToken: false # disables automatic Mount

#pod-definition.yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-kubernetes-dashboard
spec:
  containers:
    - name: my-kubernetes-dashboard
      image: my-kubernetes-dashboard
  serviceAccountName: dashboard-sa
```
