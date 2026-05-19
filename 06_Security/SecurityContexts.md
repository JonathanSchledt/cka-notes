# Security Contexts

## Concept

Security Settings at Pod or Container Level

Container Settings overwrite Pod Settings

## Key Commands

```bash
whoami
```

## Minimal YAML Example

```yaml
# Security Context at Pod level
apiVersion: v1
kind: Pod
metadata:
  name: web-pod
spec:
  securityContext:
    runAsUser: 1000 # root user is 0
  containers:
    - name: ubuntu
      image: ubuntu
      command: ["sleep", "3600"]

# Security Context at Container level
apiVersion: v1
kind: Pod
metadata:
  name: web-pod
spec:
  containers:
    - name: ubuntu
      image: ubuntu
      command: ["sleep", "3600"]
      securityContext:
        runAsUser: 1000
        capabilities: # capabilities only supported at container level and not at the Pod level
          add: ["MAC_ADMIN"]
```
