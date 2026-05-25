# Inspection

## Concept

Fast ways to find what's broken

## Key Commands

```bash
# events - sort by time
k get events --sort-by=.lastTimestamp

k get events -n kube-system --sort-by=.lastTimestamp

# events for one object
k get events --field-selector involvedObject.name=mypod

# wide output (node, IP)
k get pods -o wide

# all resources in ns
k get all -n dev

# include "not common" resources
k get all,cm,secret,ing,pvc -n dev

# watch
k get pods -w

# describe is your friend
k describe pod mypod | less

# logs
k logs mypod
k logs mypod -c container-name
k logs mypod --previous
k logs -l app=web --tail=50

# exec
k exec -it mypod -- sh
k exec mypod -- env

# debug pod for troubleshooting
k run tmp --image=busybox --rm -it --restart=Never -- sh
k run tmp --image=nicolaka/netshoot --rm -it --restart=Never -- sh

# rbac check
k auth can-i create pods
k auth can-i '*' '*' --as system:serviceaccount:dev:app-sa
```
