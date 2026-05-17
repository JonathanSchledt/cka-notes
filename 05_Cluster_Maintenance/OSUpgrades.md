# Operating System Upgrade

## Concept

Taking down nodes that are part of the cluster for maintenance (upgrading base software, applying securty patches etc.)

## Key Commands

```bash
# evict pods from nodes and disallows scheduling to node
k drain node-1

# allows pods to be scheduled to node
k uncordon node-1

# no pods can be scheduled to node
k cordon node-2
```
