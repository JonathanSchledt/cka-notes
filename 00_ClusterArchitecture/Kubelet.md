# Kubelet

## Concept

Runs on every Node (Master + Worker)

- Registers Node with cluster
- Receives Pod specs from kube-apiserver
- Talks to container runtime (CRI) to start/stop containers
- Reports Node and Pod status back to kube-apiserver

NOT installed by kubeadm -> Must be installed manually on each Node

## Key Commands

```bash
service kubelet status

systemctl restart kubelet

# kubelet config
cat /var/lib/kubelet/config.yaml

# kubelet kubeconfig (talks to apiserver)
cat /etc/kubernetes/kubelet.conf

# logs
journalctl -u kubelet -f

# systemd unit
cat /etc/systemd/system/kubelet.service.d/10-kubeadm.conf
```
