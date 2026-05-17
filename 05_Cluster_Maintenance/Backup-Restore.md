# Backup and Restore Methods

## Concept

Backup Candidates:

- Resource Configuration

- etcd Cluster

- Persistent Volumes

## Key Commands

```bash
# Resource Configuration
k get all --all-namespaces -o yaml > all-deploy-services.yaml

# etcd
etcdctl --endpoints=https://[127.0.0.1]:2379 \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
snapshot save snapshot.db

etcdctl snapshot status snapshot.db

# Restore from etcd
systemctl stop kube-apiserver

etcdctl snapshot restore snapshot.db --data-dir /var/lib/etcd-from-backup

systemctl daemon-reload

systemctl restart etcd

systemctl start kube-apiserver
```

/etc/kubernetes/pki/etcd/server.crt

/etc/kubernetes/pki/etcd/ca.crt
