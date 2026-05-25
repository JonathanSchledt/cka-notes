# Kubectl Debug

## Concept

Three modes:

1. Ephemeral container: attach a debug container to a running Pod (no restart)
2. Copy of Pod: clone a Pod with debug image / different command
3. Node debug: launch a privileged Pod on a Node with host filesystem mounted at /host

Useful when the original container is distroless or has no shell

## Key Commands

```bash
# attach ephemeral container to running Pod
k debug -it mypod --image=busybox --target=app

# copy of a Pod with a shell
k debug mypod -it --image=busybox --share-processes --copy-to=mypod-debug

# Node debug (drops you on the Node)
k debug node/worker-1 -it --image=busybox
# host filesystem mounted at /host
chroot /host

# clean up
k delete pod mypod-debug
k delete pod node-debugger-worker-1-xxxx
```
