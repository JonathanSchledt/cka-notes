# Kube API Server

## Concept

Frontend of the Control Plane

Handles: Authentication -> Authorization -> Admission Controllers -> Validation -> etcd

Only component that talks to etcd directly

## Key Commands

```bash
# view configuration
cat /etc/kubernetes/manifests/kube-apiserver.yaml

# systemd-based setup
cat /etc/systemd/system/kube-apiserver.service

ps -aux | grep kube-apiserver
```

## Minimal YAML Example

```yaml
# /etc/kubernetes/manifests/kube-apiserver.yaml
apiVersion: v1
kind: Pod
metadata:
  name: kube-apiserver
  namespace: kube-system
spec:
  containers:
    - command:
        - kube-apiserver
        - --advertise-address=172.17.0.11
        - --authorization-mode=Node,RBAC
        - --client-ca-file=/etc/kubernetes/pki/ca.crt
        - --etcd-servers=https://127.0.0.1:2379
        - --service-cluster-ip-range=10.96.0.0/12
        - --enable-admission-plugins=NodeRestriction
      image: k8s.gcr.io/kube-apiserver:v1.30.0
      name: kube-apiserver
```
