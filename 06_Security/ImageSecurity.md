# Image Security

## Concept

image: docker.io/library/nginx (gcr.io/kubernetes-e2e-test-images/dnsutils)

docker.io -> registry

library -> User/Account

nginx -> Image/Repository

## Key Commands

```bash
k create secret docker-registry regcred \
  --docker-server=private-registry.io \
  --docker-username=registry-user \
  --docker-password=registry-password \
  --docker-email=registry-user@org.com

k get secret
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx
      image: private-registry.io/apps/internal-app
  imagePullSecrets:
    - name: regcred
```
