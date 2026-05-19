# Persistent Volume

## Concept

Cluster wide Volume

Reclaim Policies:

- Retain: Keeps PV and it's data

- Delete: Deletes PV

- Recycle (Deprecated): Data is scrubbed and PV is made available for claims again

## Key Commands

```bash
k get pv
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-vol1
spec:
  accessModes:
    - ReadWriteOnce
  capacity:
    storage: 1Gi
  persistentVolumeReclaimPolicy: Retain
  awsElasticBlockStore:
    volumeID: <volume-id>
    fsType: ext4

# pod-definition.yaml
apiVersion: v1
kind: Pod
metadata:
 name: mypod
spec:
 containers:
  - name: myfrontend
   image: nginx
   volumeMounts:
   - mountPath: "/var/www/html"
    name: mypd
 volumes:
  - name: mypd
   persistentVolumeClaim:
    claimName: myclaim
```
