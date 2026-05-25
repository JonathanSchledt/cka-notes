# JSON Path

## Concept

Using JSON Path in kubectl

1. Identify the kubectl command

2. Familiarize with JSON output

3. Form the JSON Path query

4. Use the JSON Path query with the kubectl command

## Key Commands

```bash
k get pods -o=jsonpath='{.items[0].spec.containers[0].image}'

k get nodes -o=jsonpath='{.items[*].metadata.name} {"\n"} {.items[*].status.capacity.cpu}'

# loops
k get nodes -o=jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.status.capacity.cpu}{"\n"}{end}'

#custom columns
k get nodes -o=custom-columns=NODE:.metadata.name,CPU:.status.capacity.cpu

k get nodes --sort-by=.metadata.name

# custom queries
k config view --kubeconfig=my-kube-config -o jsonpath="{.contexts[?(@.context.user=='aws-user')].name}"
```
