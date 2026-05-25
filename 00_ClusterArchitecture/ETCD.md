# ETCD

## Concept

Distributed Key-Value Store - Cluster source of truth

Stored under /registry

Default port: 2379

Deployed as Static Pod (kubeadm) or external cluster

## Key Commands

```bash
# inside etcd pod / on node with etcdctl
ETCDCTL_API=3 etcdctl \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  member list

# list all keys
etcdctl get / --prefix --keys-only

# snapshot
etcdctl snapshot save /opt/snapshot.db

etcdctl snapshot status /opt/snapshot.db
```

## Minimal YAML Example

```yaml
# /etc/kubernetes/manifests/etcd.yaml
apiVersion: v1
kind: Pod
metadata:
  name: etcd
  namespace: kube-system
spec:
  containers:
    - command:
        - etcd
        - --advertise-client-urls=https://172.17.0.11:2379
        - --cert-file=/etc/kubernetes/pki/etcd/server.crt
        - --key-file=/etc/kubernetes/pki/etcd/server.key
        - --data-dir=/var/lib/etcd
        - --listen-client-urls=https://127.0.0.1:2379,https://172.17.0.11:2379
        - --trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt
      image: k8s.gcr.io/etcd:3.5.10-0
      name: etcd
```
