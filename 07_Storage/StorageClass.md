# Storage Class

## Concept

Dynamic Provisioning of volumes: Ability to define a provisioner that can automatically provision sotrage and attach that to pods when a claim is made

No more PV needed (PV is still created, it just doesn't need to be created manually)

## Key Commands

```bash
k get sc
```

## Minimal YAML Example

```yaml
# storage class
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: google-storage
provisioner: kubernetes.io/gce-pd

# pvc
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myclaim
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: google-storage
  resources:
    requests:
      storage: 500Mi
```
