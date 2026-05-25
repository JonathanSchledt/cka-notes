# Role-Based Access Control

## Concept

1. Create Role

2. Bind User to Role

Namespaced (default ns if not provided)

## Key Commands

```bash
# list namespaces resources
k api-resources --namespaced=true

k apply -f developer-role.yaml

k apply -f devuser-developer-binding.yaml

k get roles

k get rolebindings

k auth can-i create deployments

k auth can-i create pods --as dev-user

k auth can-i create pods --as dev-user --namespace test
```

## Minimal YAML Example

```yaml
# developer-role.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: developer
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["list", "get", "create", "update", "delete"]
    resourceNames: ["blue", "orange"]
  - apiGroups: [""]
    resources: ["configmaps"]
    verbs: ["create"]

# devuser-developer-binding.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: devuser-developer-binding
subjects:
- kind: User
  name: dev-user
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: developer
  apiGroup: rbac.authorization.k8s.io

# bind a Role to a ServiceAccount (more common in practice)
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: app-sa-binding
  namespace: dev
subjects:
  - kind: ServiceAccount
    name: app-sa
    namespace: dev
roleRef:
  kind: Role
  name: developer
  apiGroup: rbac.authorization.k8s.io
```

## Built-in Cluster Roles

- view: read-only
- edit: read/write most resources (no RBAC)
- admin: full namespace admin (no RBAC, no resource quota)
- cluster-admin: full cluster access
