# Kube Controller Manager

## Concept

Runs all built-in controllers as a single process

Controllers (watch loops):

- Node Controller: Monitors Node status (5s, 40s grace, 5min eviction)
- Replication Controller: Ensures desired replica count
- Endpoint Controller: Joins Services and Pods
- ServiceAccount Controller, Namespace Controller, Job Controller, ...

## Key Commands

```bash
cat /etc/kubernetes/manifests/kube-controller-manager.yaml

k logs kube-controller-manager-master -n kube-system

ps -aux | grep kube-controller-manager
```

## Minimal YAML Example

```yaml
# /etc/kubernetes/manifests/kube-controller-manager.yaml
apiVersion: v1
kind: Pod
metadata:
  name: kube-controller-manager
  namespace: kube-system
spec:
  containers:
    - command:
        - kube-controller-manager
        - --kubeconfig=/etc/kubernetes/controller-manager.conf
        - --cluster-cidr=10.244.0.0/16
        - --service-cluster-ip-range=10.96.0.0/12
        - --node-monitor-period=5s
        - --pod-eviction-timeout=5m0s
      image: k8s.gcr.io/kube-controller-manager:v1.30.0
      name: kube-controller-manager
```
