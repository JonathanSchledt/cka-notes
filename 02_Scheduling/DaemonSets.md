# DaemonSets

## Concept
One copy of each Pod one each Node

Uses NodeAffinity and Default Scheduler

Monitoring-Agents
Kube-Proxy
Networking (calico)

## Key Commands

```bash
k create -f daemon-set-definition.yaml

k get ds

#tip: change deployment to daemonset
k create deployment
```

## Minimal YAML Example

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: monitoring-daemon
spec:
  selector:
    matchLabels:
      app: monitoring-agent
  template:
    metadata:
      labels:
        app: monitoring-agent
    spec:
      containers:
        - name: monitoring-agent
          image: monitoring-agent
```
