# Service Networking

## Concept

Service: Virtual Cluster wide Objects

## Key Commands

```bash
# rules created by kube-proxy
iptables -L -t nat | grep my-service

# kube-proxy logs
cat /var/log/kube-proxy
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Example
metadata:
  name: example
spec:
  # ...
```
