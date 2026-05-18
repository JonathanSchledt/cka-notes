# Cluster Roles

## Concept

1. Create Cluster Role

2. Bind User to Cluster Role

Cluster scoped (not namespaced)

Possibility to give namespaced roles as well

## Key Commands

```bash
# list cluster scoped resources
k api-resources --namespaced=false

k get clusterroles

k get clusterrolebindings

k apply -f cluster-admin-role.yaml

k apply -f cluster-admin-role-binding.yaml
```

## Minimal YAML Example

```yaml
# cluster-admin-role.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: cluster-administrator
rules:
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["list", "get", "create", "delete"]

# cluster-admin-role-binding.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: cluster-admin-role-binding
subjects:
- kind: User
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: cluster-administrator
  apiGroup: rbac.authorization.k8s.io
```
