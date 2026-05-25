# Kube Scheduler

## Concept

Decides which Node a Pod runs on - does NOT actually place the Pod (kubelet does)

Two phase:

1. Filtering: Find Nodes that fit (resources, taints, affinity)
2. Scoring: Rank fitting Nodes, pick highest

## Key Commands

```bash
cat /etc/kubernetes/manifests/kube-scheduler.yaml

k logs kube-scheduler-master -n kube-system

# manually bind a Pod when no scheduler exists
k get pods --all-namespaces | grep scheduler
```

## Minimal YAML Example

```yaml
# /etc/kubernetes/manifests/kube-scheduler.yaml
apiVersion: v1
kind: Pod
metadata:
  name: kube-scheduler
  namespace: kube-system
spec:
  containers:
    - command:
        - kube-scheduler
        - --kubeconfig=/etc/kubernetes/scheduler.conf
        - --leader-elect=true
      image: k8s.gcr.io/kube-scheduler:v1.30.0
      name: kube-scheduler
```
