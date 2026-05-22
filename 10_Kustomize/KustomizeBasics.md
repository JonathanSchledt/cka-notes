# Kustomize Basics

## Concept

Customize environments instead of repeating files

base config: identical across environments + default values

overlays: one for each env

Kustomize creates the final manifests out of the base config and the overlays

## Key Commands

```bash
kustomize build k8s/ #directory where the kustomization.yaml file is

kustomize build k8s/ | k apply -f - # applies the changes
k apply -k k8s/

kustomize build k8s/ | k delete -f -
k delete -k k8s/
```

## Minimal YAML Example

```yaml
# kustomization.yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
resources:
  - nginx-deployment.yaml
  - nginx-service.yaml
commonLabels:
  company: KodeKloud
```
