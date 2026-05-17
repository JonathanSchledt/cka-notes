# Commands and Arguments

## Concept

Docker:

- Entrypoint: Command Line arguments will be appended

Kubernets:

- command: -> overwrites Docker image Entrypoint instruction
- args: -> overwrites Docker image CMD instruction

## Key Commands

```bash
# docker run ubuntu-sleeper -> sleep 5
# docker run ubuntu-sleeper 10 -> sleep 10
# docker run --entrypoint sleep2.0 ubuntu-sleeper 10 -> sleep2.0 10
FROM Ubuntu
ENTRYPOINT ["sleep"]
CMD["5"]
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-sleeper-pod
spec:
  containers:
    - name: ubuntu-sleeper
      image: ubuntu-sleeper
      command: ["sleep2.0"]
      args: ["10"]
```
