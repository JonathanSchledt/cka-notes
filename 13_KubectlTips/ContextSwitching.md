# Context Switching

## Concept

Exam has multiple clusters - wrong context = zero points

ALWAYS run the `kubectl config use-context` shown at the top of each question first

## Key Commands

```bash
# list / current
k config get-contexts
k config current-context

# switch cluster
k config use-context cluster-1

# switch default namespace for current context
k config set-context --current --namespace=dev

# ssh to node for control plane / kubelet tasks
ssh node01
sudo -i

# back to bastion
exit
```
