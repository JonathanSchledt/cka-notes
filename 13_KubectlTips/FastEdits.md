# Fast Edits

## Concept

Modify running resources without writing YAML

Most fields can be patched - some (e.g. selector) require delete + recreate

## Key Commands

```bash
# edit live resource
k edit deployment web

# scale
k scale deployment web --replicas=5

# set image (rolling update)
k set image deployment/web nginx=nginx:1.25

# set env / resources
k set env deployment/web LOG_LEVEL=debug
k set resources deployment/web --limits=cpu=200m,memory=256Mi

# label / annotate
k label pod nginx env=prod
k annotate pod nginx owner=team-a

# patch
k patch deployment web -p '{"spec":{"replicas":3}}'

# force replace (delete + recreate from file)
k replace -f pod.yaml --force

# delete fast
k delete pod nginx --force --grace-period=0

# vim: indent yaml properly (run before pasting)
# :set paste
# :set et ts=2 sw=2 ai
```
