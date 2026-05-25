# Network Troubleshooting

## Concept

Troubleshooting Order:

1. Pods

2. Services

3. CoreDNS

4. CNI

5. kube-proxy

## Key Commands

```bash
# -l: label
k get pods -l app=hostnames

# try to curl the pod from a temporary pod
k run -it --rm --restart=Never busybox --image=busybox sh

k get svc hostnames -o yaml

k get endpointslices -l kbuernetes.io/service-name=hostnames -n default

k get pods -n kube-system -l k8s-app=kube-dns

k get endpointslice -l k8s.io/service-name=kube-dns -n kube-system

k exec -it <pod-name> --cat /etc/resolv.conf

k exec -it busybox -- nslookup kubernetes.default.svc.cluster.local

k exec -it -- nslookup my-app-service.default.svc.cluster.local

# Troubleshooting kube-proxy Issues
k get pods -n kube-system -l k8s-app=kube-proxy

k logs kube-proxy-abc-12 -n kube-system

k get configmap kube-proxy -n kube-system -o yaml

ipvsadm -ln
```
