# Control Plane Failure

## Key Commands

```bash
k get nodes

k get pods

k get pods -n kube-system

service kube-apiserver status

service kube-contoller-manager status

service kube-scheduler status

service kubelet status

service kube-proxy status

k logs kube-apiserver-master -n kube-system

sudo journalctl -u kube-apiserver
```
