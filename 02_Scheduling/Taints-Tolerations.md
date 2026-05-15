# Taints and Tolerations

## Concept
- Set Restrcitions on which Pods can be scheduled on which Nodes
- Pods have no Tolerations by default

Taint: Set on Nodes
Toleration: Set on Pods

Taint-Effects:
- No Schedule
- PreferNoSchedule
- NoExecute

Doesnt guarantee Pods being scheduled on certain Nodes -> NodeAffinity

Taint is set on Master Node automatically

## Key Commands

```bash
k taint nodes node-name key=value:taint-effect

k taint nodes node1 app=myapp:NoSchedule

k describe node controlplane | grep Taints
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
    - name: nginx-container
      image: nginx
  tolerations:
    - key: "app"
      operator: "Equal"
      value: "blue"
      effect: "NoSchedule"
```
