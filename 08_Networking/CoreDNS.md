# CoreDNS

## Concept

Deployed as Pod in kube-system namespace (as replicaset in deployment)

## Key Commands

```bash
# address service within namespace
curl hhtp://web-servce

# address service outside namespace
curl http://web-service.app.scv.cluster.local

# points to the DNS server
cat /etc/resolv.conf

# IP of cluster DNS
cat /var/lib/kubelet/config.yaml

cat /etc/coredns/Corefile # or: k describe cm coredns -n kube-system
```

```json
.:53 {
    errors
    health

    kubernetes cluster.local in-addr.arpa ip6.arpa {
        pods insecure
        upstream
        fallthrough in-addr.arpa ip6.arpa
    }

    prometheus :9153

    proxy . /etc/resolv.conf

    cache 30

    reload
}
```
