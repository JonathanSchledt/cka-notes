# Service Networking

## Concept

Service: Virtual Cluster wide Objects

IP ranges configured in /etc/kubernetes/manifests/kube-controller-manager.yaml

## Key Commands

```bash
# rules created by kube-proxy
iptables -L -t nat | grep my-service

# kube-proxy logs
cat /var/log/kube-proxy
```
