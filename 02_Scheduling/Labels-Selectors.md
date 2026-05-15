# Labels and Selectors

## Concept
Group Objects
Used in ReplicaSets, Services

Annotations record other details

## Key Commands

```bash
k get pods --selector app=App1

#logical and
k get all --selector env=prod,bu=finance,tier=frontend
```
