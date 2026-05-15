# Manual Scheduling

## Concept
(Schedule) Bind Pod to Node
Can only be manually set during Pod creation

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Example
metadata:
  name: example
spec:
  nodeName: node02
```
