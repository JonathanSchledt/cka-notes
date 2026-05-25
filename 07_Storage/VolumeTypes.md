# Volume Types

## Concept

Common Pod-level volume sources (no PV/PVC needed)

- emptyDir: Empty dir on Node, deleted with Pod (scratch space, sharing between containers in same Pod)
- hostPath: Mount path from Node (avoid in production)
- configMap: Mount ConfigMap keys as files
- secret: Mount Secret keys as files
- projected: Combine multiple sources into one mount
- downwardAPI: Expose Pod metadata as files

subPath: Mount a single file/dir from a volume instead of the whole volume

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: vol-demo
spec:
  containers:
    - name: app
      image: nginx
      volumeMounts:
        # configMap as volume
        - name: cfg
          mountPath: /etc/app/config.yaml
          subPath: config.yaml # mount single key
        # secret as volume
        - name: tls
          mountPath: /etc/tls
          readOnly: true
        # emptyDir for scratch
        - name: cache
          mountPath: /cache
  volumes:
    - name: cfg
      configMap:
        name: app-config
        items:
          - key: config.yaml
            path: config.yaml
    - name: tls
      secret:
        secretName: tls-secret
        defaultMode: 0400
    - name: cache
      emptyDir:
        sizeLimit: 500Mi
        # medium: Memory # tmpfs
```
