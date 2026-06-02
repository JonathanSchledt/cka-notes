# Helm Components

## Concept

- Helm CLI – command-line tool used to manage charts and releases
- Chart – a collection of templated YAML files that describe a set of Kubernetes resources
- Release – a running instance of a chart deployed to a cluster
- Artifact Hub – public repository to discover and share Helm charts

## Key Commands

```bash
# search for charts on Artifact Hub
helm search hub wordpress

# search in added repos
helm search repo wordpress

helm repo add bitnami https://charts.bitnami.com/bitnami

helm repo remove bitnami

helm repo list

helm list

helm pull --untar bitnami/wordpress
```

## Minimal YAML Example

```yaml
# values.yaml
replicaCount: 1
image:
  repository: nginx
```
