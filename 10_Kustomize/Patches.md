# Patches

## Concept

Provides a more surgical approach to targeting one or more specific sections in a Kubernetes resource

operators: add, replace, remove

## Key Commands

```bash
kustomize build k8s/overlays/dev

k apply -k k8s/overlays/dev
```

## Minimal YAML Example

```yaml
# kustomization.yaml - JSON 6902 Patch
patches:
  - target:
      kind: Deployment
      name: api-deployment
    patch: |-
      - op: replace
        path: /metadata/name
        value: web-deployment

# kustomization.yaml - strategic merge
resources:
  - api-depl.yaml

patches:
  - path: api-patch.yaml

# api-patch.yaml - strategic merge
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-deployment
spec:
  template:
    spec:
      containers:
        - $patch: delete
          name: memcached
```
