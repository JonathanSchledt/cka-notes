# Lifecycle Management

## Concept

Helm tracks every install, upgrade, and rollback as a numbered revision. Use `helm history` to view revisions and `helm rollback` to revert to a previous one.

## Key Commands

```bash
helm install nginx-release bitnami/nginx

helm upgrade nginx-release bitnami/nginx --set replicaCount=3

helm history nginx-release

helm rollback nginx-release 1

helm status nginx-release

helm uninstall nginx-release
```
