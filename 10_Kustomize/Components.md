# Components

## Concept

Components provide the ability to define reusable pieces of configuration logic (resources + patches) that can be included in multiple overlays

```text
k8s/
├── base/
│   ├── kustomization.yaml
│   └── api-depl.yaml
│
├── components/
│   ├── caching/
│   │   ├── kustomization.yaml
│   │   ├── deployment-patch.yaml
│   │   └── redis-depl.yaml
│   │
│   └── db/
│       ├── kustomization.yaml
│       ├── deployment-patch.yaml
│       └── postgres-depl.yaml
│
└── overlays/
    ├── dev/
    │   └── kustomization.yaml
    │
    ├── premium/
    │   └── kustomization.yaml
    │
    └── standalone/
        └── kustomization.yaml
```

## Key Commands

```bash
kustomize build k8s/overlays/premium

k apply -k k8s/overlays/premium
```

## Minimal YAML Example

```yaml
# db/kustomization.yaml
apiVersion: kustomize.config.k8s.io/v1alpha1
kind: Component
resources:
  - postgres-depl.yaml
secretGenerator:
  - name: postgres-cred
    literals:
      - password=postgres123
patches:
  - deployment-patch.yaml

# premium/kustomization.yaml
bases:
  - ../../base
components:
  - ../../components/db
```
