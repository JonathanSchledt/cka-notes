# Control Plane

## Concept

Control Plane runs on Master Node(s)

Components:

- kube-apiserver: Frontend for the cluster, all communication goes through it
- etcd: Key-Value store for all cluster data
- kube-scheduler: Assigns Pods to Nodes
- kube-controller-manager: Runs controllers (Node, Replication, Endpoint, ServiceAccount)
- cloud-controller-manager: Interacts with underlying cloud provider

kubeadm setup -> Components run as Static Pods in kube-system namespace

## Key Commands

```bash
k get pods -n kube-system

# manifests of static pod components
ls /etc/kubernetes/manifests

# logs of control plane components
k logs kube-apiserver-master -n kube-system

# systemd-based setups
journalctl -u kube-apiserver
journalctl -u kube-controller-manager
journalctl -u kube-scheduler
```
