# Network Policies

## Concept

Firewall rules at Pod level - only enforced if CNI supports it

Supported: Calico, Cilium, Kube-router, Weave - NOT Flannel

Pods are non-isolated by default (allow all). A NetworkPolicy selecting a Pod switches it to deny-by-default for the listed `policyTypes`.

AND vs OR (the exam trap):

- Items in the same `from`/`to` list element = AND (Pod must match podSelector AND namespaceSelector)
- Separate list elements (each prefixed with `-`) = OR

## Key Commands

```bash
k get netpol

k describe netpol db-policy

# test from a temp Pod
k run tmp --image=busybox --rm -it --restart=Never -- wget -qO- --timeout=2 db:3306
```

## Minimal YAML Example

```yaml
# default deny all ingress in a namespace
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny-ingress
spec:
  podSelector: {}
  policyTypes:
    - Ingress

# default deny all egress
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny-egress
spec:
  podSelector: {}
  policyTypes:
    - Egress

# allow specific traffic (AND vs OR)
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-policy
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
    - Ingress
    - Egress
  ingress:
    - from:
        # AND: Pod labeled api-pod IN namespace prod
        - podSelector:
            matchLabels:
              name: api-pod
          namespaceSelector:
            matchLabels:
              kubernetes.io/metadata.name: prod
        # OR: any Pod from this CIDR
        - ipBlock:
            cidr: 192.168.5.10/32
      ports:
        - protocol: TCP
          port: 3306
  egress:
    - to:
        - ipBlock:
            cidr: 192.168.5.10/32
      ports:
        - protocol: TCP
          port: 80
    # allow DNS (almost always needed when egress is restricted)
    - to:
        - namespaceSelector: {}
          podSelector:
            matchLabels:
              k8s-app: kube-dns
      ports:
        - protocol: UDP
          port: 53
```
