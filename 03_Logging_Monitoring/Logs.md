# Managing Application Logs

## Concept

Docker Logs used

Multiple images in the Pod -> Image has to be specified

## Key Commands

```bash
#Pod with single image
k logs -f event-simulator-pod

#Pod with multiple images
k logs -f event-simulator-pod event-simulator
```

## Minimal YAML Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: event-simulator-pod
spec:
  containers:
    - name: event-simulator
      image: kodekloud/event-simulator
    - name: image-processor
      image: some-image-processor
```
