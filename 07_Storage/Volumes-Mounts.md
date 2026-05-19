# Volumes and Mounts

## Concept

Mount volumes to a host/external provider

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: random-number-generator
spec:
  containers:
    - image: alpine
      name: alpine
      command: ["/bin/sh", "-c"]
      args: ["shuf -i 0-100 -n 1 >> /opt/number.out;"]
      volumeMounts:
        - mountPath: /opt
          name: data-volume
  volumes:
    - name: data-volume
      hostPath: # shouldn't be used in production environment
        path: /data
        type: Directory
#   - name: data-volume
#     awsElasticBlockStore:
#       volumeID: <volume-id>
#       fsType: ext4
```
