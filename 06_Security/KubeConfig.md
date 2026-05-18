# Kube Config

## Concept

KubeConfig File ($HOME/.kube/config)

- Clusters (Development, Google)
- Contexts (Admin@Development, Dev@Google)
- Users (Admin, Dev)

## Key Commands

```bash
k config view

k config view -kubeconfig=my-custom-config

k config use-context prod-user@production
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Config
current-context: admin@production
clusters:
  - name: production
    cluster:
      certificate-authority: ca.crt
      server: https://172.17.0.51:6443
contexts:
  - name: admin@production
    context:
      cluster: production
      user: admin
      namespace: finance
users:
  - name: admin
    user:
      client-certificate: admin.crt
      client-key: admin.key
```
