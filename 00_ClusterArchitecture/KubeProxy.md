# Kube Proxy

## Concept

Runs on every Node (DaemonSet in kube-system)

Implements Service abstraction -> Creates rules so Service IP forwards to Pod IPs

Modes:

- iptables (default)
- ipvs (scales better)

## Key Commands

```bash
k get ds kube-proxy -n kube-system

k logs kube-proxy-abc12 -n kube-system

# iptables rules created by kube-proxy
iptables -L -t nat | grep my-service

# ipvs mode
ipvsadm -ln

# kube-proxy config
k get cm kube-proxy -n kube-system -o yaml
```
