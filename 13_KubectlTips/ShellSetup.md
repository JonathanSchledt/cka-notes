# Shell Setup

## Concept

First thing to run on exam terminal - saves time on every command

## Key Commands

```bash
# alias
alias k=kubectl

# dry-run shortcut
export do='--dry-run=client -o yaml'

# force-delete shortcut
export now='--force --grace-period=0'

# usage
k run nginx --image=nginx $do > nginx.yaml
k delete pod nginx $now

# autocomplete (usually pre-configured)
source <(kubectl completion bash)
complete -F __start_kubectl k

# bash history search
# Ctrl+R then type a fragment
```
