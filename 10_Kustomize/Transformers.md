# Transformers

## Concept

commonLabel: adds a label to all Kubernetes resources

namePrefix/Suffix: adds a common prefix-suffix to all resource names

Namespace: adds a common namespace to all resources

commonAnnotations: adds an annotation to all resources

Image Transformer: change the image or the tag

## Key Commands

```bash
kustomize build k8s/

k apply -k k8s/
```

## Minimal YAML Example

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
resources:
  - nginx-deployment.yaml
  - nginx-service.yaml
namePrefix: KodeKloud-
nameSuffix: -web
commonAnnotations:
  logging: verbose
images:
  - name: mongo # name of the image
    newTag: "4.2"
```
