# Overlays

## Concept

Environment specific overwrites of the base configuration

Possibility to add new configs

## Common Structure

```text
k8s/
├── base/
│   ├── kustomization.yaml
│   ├── nginx-depl.yaml
│   ├── service.yaml
│   └── redis-depl.yaml
│
└── overlays/
    ├── dev/
    │   ├── kustomization.yaml
    │   └── config-map.yaml
    │
    ├── stg/
    │   ├── kustomization.yaml
    │   └── config-map.yaml
    │
    └── prod/
        ├── kustomization.yaml
        └── config-map.yaml
```

## Key Commands

```bash
kustomize build k8s/overlays/dev

k apply -k k8s/overlays/dev
```

## Minimal YAML Example

```yaml
# dev/kustomization
bases:
  - ../../base
patch: |-
  - op: replace
    path: /spec/replicas
    value: 2
```
