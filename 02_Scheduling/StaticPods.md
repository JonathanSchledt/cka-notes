# Static Pods

## Concept
Kubelet works at a Pod-Level

Kubelet can manage a Pod individually

Static Pods creates a mirror object in kube-apiserver

Use-Case: Configure Master-Node (kubeadm tool does this)

## Key Commands

```bash
#in kubelet file (/usr/local/bin/kubelet)
--pod-manifest-path=/etc/kubernetes/manifests

#or in /var/lib/kubelet/config.yaml

#in kubeconfig (/usr/local/bin/kubelet)
--config=kubeconfig.yaml

#in kubeconfig.yaml
staticPodPath: /etc/kubernetes/manifests
```