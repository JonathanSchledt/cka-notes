# Worker Node Failure

## Key Commands

```bash
k get nodes

k describe node worker-1

# checking node
top
df -h

service kubelet status

sudo journalctl -u kubelet

openssl x509 -in /var/lib/kubelet/worker-1.crt
```
