# Application Failure

## Concept

Common Pod status decode:

- Pending: scheduler couldn't place it (resources, taints, affinity, PVC unbound)
- ContainerCreating: scheduled, image pulling or volume attaching
- ImagePullBackOff / ErrImagePull: registry auth, wrong image name/tag
- CrashLoopBackOff: container starts then exits - check logs --previous
- CreateContainerConfigError: missing ConfigMap/Secret referenced in env/volumes
- OOMKilled: hit memory limit
- Error / Completed: exited - non-zero / zero

Troubleshooting order: events -> describe -> logs (current + previous) -> exec

## Key Commands

```bash
# events first
k get events --sort-by=.lastTimestamp

k get events --field-selector involvedObject.name=mypod

# describe shows scheduling + probe + image errors
k describe pod mypod

# logs
k logs mypod
k logs mypod --previous
k logs mypod -c sidecar

# service / endpoints sanity
k get svc,ep web-service

k describe service web-service

# from inside cluster
k run tmp --image=busybox --rm -it --restart=Never -- wget -qO- web-service
```
