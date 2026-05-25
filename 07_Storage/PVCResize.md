# PVC Resize

## Concept

Expand a PVC without recreating it

Requirements:

- StorageClass has `allowVolumeExpansion: true`
- Underlying storage driver supports expansion
- Only increase, never shrink

Pod may need restart for filesystem to resize (online resize supported by some drivers)

## Key Commands

```bash
# edit PVC and bump spec.resources.requests.storage
k edit pvc myclaim

# or patch
k patch pvc myclaim -p '{"spec":{"resources":{"requests":{"storage":"5Gi"}}}}'

# check status
k get pvc myclaim
k describe pvc myclaim | grep -i condition
```
