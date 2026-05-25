# Dry Run

## Concept

Generate YAML imperatively - never hand-write from scratch

Pattern: imperative command + `--dry-run=client -o yaml` > file, then edit

## Key Commands

```bash
# pod
k run nginx --image=nginx --dry-run=client -o yaml > pod.yaml

# pod with port, env, command
k run nginx --image=nginx --port=80 --env=APP=blue \
  --dry-run=client -o yaml > pod.yaml

k run busy --image=busybox --dry-run=client -o yaml \
  --command -- sleep 3600 > pod.yaml

# deployment
k create deployment web --image=nginx --replicas=3 \
  --dry-run=client -o yaml > deploy.yaml

# service
k expose pod nginx --port=80 --target-port=8080 \
  --dry-run=client -o yaml > svc.yaml

k create service clusterip my-svc --tcp=80:8080 \
  --dry-run=client -o yaml > svc.yaml

# configmap / secret
k create cm app-config --from-literal=KEY=value \
  --dry-run=client -o yaml > cm.yaml

k create secret generic app-secret --from-literal=PW=pass \
  --dry-run=client -o yaml > secret.yaml

# job / cronjob
k create job hello --image=busybox \
  --dry-run=client -o yaml -- echo hi > job.yaml

k create cronjob hello --image=busybox --schedule="*/1 * * * *" \
  --dry-run=client -o yaml -- echo hi > cj.yaml

# rbac
k create role dev --resource=pods --verb=get,list,create \
  --dry-run=client -o yaml > role.yaml

k create rolebinding dev-bind --role=dev --user=jane \
  --dry-run=client -o yaml > rb.yaml

k create clusterrole node-reader --resource=nodes --verb=get,list \
  --dry-run=client -o yaml > cr.yaml

# namespace / serviceaccount
k create ns dev --dry-run=client -o yaml > ns.yaml
k create sa app-sa --dry-run=client -o yaml > sa.yaml

# ingress
k create ingress web --rule="example.com/*=web-svc:80" \
  --dry-run=client -o yaml > ing.yaml
```
