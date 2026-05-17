# Cluster Upgrade

## Concept

Nodes can be upgraded one at a time with drain node und uncordon node

## Key Commands

```bash
kubeadm upgrade plan

# upgrade master node
apt-get upgrade -y kubeadm=1.12.0-00

kubeadm upgrade apply v1.12.0

apt-get upgrade -y kubelet=1.12.0-00

systemctl restart kubelet

# upgrade worker node
k drain node-1

apt-get upgrade -y kubeadm=1.12.0-00

apt-get upgrade -y kubelet=1.12.00-00

kubeadm upgrade node config --kubelet-version v1.12.0

systemctl restart kubelet

k uncordon node-1
```
