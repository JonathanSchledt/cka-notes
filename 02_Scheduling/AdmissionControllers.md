# Admission Controllers

## Concept

kube-apiserver -> Authentication -> Authorization -> Admission Controllers -> Create Pod

Help implement better security measures to enforce how a cluster is used

Mutating Admission Controllers: change the request -> Mutating Admission Webhook

Validation Admission Controllers: validate the request and allow or deny it -> Validating Admission Webhook

1. Deploying Webhook Server

2. Configuring Admission Webhook

## Key Commands

```bash
# view enabled admission controllers
kube-apiserver -h | grep enable-admission-plugins
```

## Minimal YAML Example

```yaml
# /etc/kubernetes/manifests/kube-apiserver.yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  name: kube-apiserver
  namespace: kube-system
spec:
  containers:
    - command:
        - kube-apiserver
        - --authorization-mode=Node,RBAC
        - --advertise-address=172.17.0.107
        - --allow-privileged=true
        - --enable-bootstrap-token-auth=true
        - --enable-admission-plugins=NodeRestriction,NamespaceAutoProvision
      image: k8s.gcr.io/kube-apiserver-amd64:v1.11.3
      name: kube-apiserver
```
