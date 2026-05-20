# Service Networking

## Key Commands

```bash
# rules created by kube-proxy
iptables -L -t nat | grep my-service

# kube-proxy logs
cat /var/log/kube-proxy
```
