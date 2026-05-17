# Rolling Updates and Rollbacks

## Concept

Types of Deployment Strategies:

- Recreate
- Rolling Update (default)

New Replicaset creating during new Deployment

## Key Commands

```bash
k rollout status deployment/myapp-deployment

k rollout history deployment/myapp-deployment

k rollout undo deployment myapp-deployment
```
