# Kubectl Explain

## Concept

In-cluster documentation - works offline, faster than browsing kubernetes.io

Use when you forget a field name or nesting

## Key Commands

```bash
k explain pod

# drill into a field
k explain pod.spec.containers

k explain deployment.spec.template.spec.containers.livenessProbe

# show all fields recursively
k explain pod --recursive

# pipe through less / grep
k explain pod.spec --recursive | less

k explain pod.spec --recursive | grep -i affinity
```
