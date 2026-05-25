# Volume Binding Mode

## Concept

When the PV gets bound to a PVC - field on StorageClass

Modes:

- Immediate (default): Bind PV as soon as PVC is created
- WaitForFirstConsumer: Bind only when a Pod using the PVC is scheduled

WaitForFirstConsumer matters for zonal storage - prevents binding a PV in zone A to a Pod scheduled in zone B

## Key Commands

```bash
k get sc

k describe sc standard
```

## Minimal YAML Example

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/aws-ebs
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true # required for PVC resize
reclaimPolicy: Delete
parameters:
  type: gp3
```
