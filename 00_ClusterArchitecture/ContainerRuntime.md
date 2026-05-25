# Container Runtime

## Concept

Runs containers on the Node - kubelet talks to it via CRI

Options: containerd (default), CRI-O

dockershim removed in v1.24 -> docker no longer a runtime

crictl: CLI to inspect containers/pods directly on the Node

## Key Commands

```bash
# CRI socket
ls /var/run/containerd/containerd.sock

# crictl - config
cat /etc/crictl.yaml

# list containers
crictl ps

crictl ps -a

# list pods
crictl pods

# logs of a container
crictl logs <container-id>

# inspect
crictl inspect <container-id>

# pull image
crictl pull nginx

# images
crictl images
```
