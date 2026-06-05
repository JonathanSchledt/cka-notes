# Kubeadm Setup

## Concept

Tool to bootstrap a cluster

Prerequisites on all Nodes: container runtime, kubeadm, kubelet, kubectl installed; swap disabled

Steps:

1. kubeadm init on Master
2. Install CNI Plugin (Calico, Flannel, ...)
3. kubeadm join on Workers

## Key Commands

```bash
# node kernel networking prerequisites (persist across reboots)
sudo tee -a /etc/sysctl.conf >/dev/null <<'EOF'
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

sudo sysctl -p

# verify
sysctl net.ipv4.ip_forward
sysctl net.bridge.bridge-nf-call-iptables

# master
kubeadm init --pod-network-cidr=10.244.0.0/16 --apiserver-advertise-address=192.168.1.10

# copy kubeconfig for current user
mkdir -p $HOME/.kube
sudo cp /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# install CNI (example: Flannel)
k apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml

# worker
kubeadm join 192.168.1.10:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>

# regenerate join command on master
kubeadm token create --print-join-command

kubeadm token list

# check cluster
k get nodes
k cluster-info
```
