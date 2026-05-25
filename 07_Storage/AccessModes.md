# Access Modes

## Concept

How a PV can be mounted - set on both PV and PVC

| Mode | Short | Meaning |
|------|-------|---------|
| ReadWriteOnce | RWO | One Node can mount read-write (multiple Pods on that Node OK) |
| ReadOnlyMany | ROX | Many Nodes can mount read-only |
| ReadWriteMany | RWX | Many Nodes can mount read-write (NFS, CephFS) |
| ReadWriteOncePod | RWOP | Single Pod cluster-wide can mount read-write (v1.22+) |

Not all storage supports all modes - block storage (EBS, GCE PD) is RWO only

## Key Commands

```bash
k get pv -o custom-columns=NAME:.metadata.name,MODES:.spec.accessModes

k get pvc -o custom-columns=NAME:.metadata.name,MODES:.spec.accessModes
```
