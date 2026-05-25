# Jobs

## Concept

Run a Pod to completion (batch task)

Fields:

- completions: how many Pods must succeed
- parallelism: how many run at once
- backoffLimit: retries before giving up (default 6)
- activeDeadlineSeconds: terminate Job after N seconds
- ttlSecondsAfterFinished: auto-cleanup

restartPolicy must be `OnFailure` or `Never`

## Key Commands

```bash
k get jobs

k logs job/my-job

# generate yaml
k create job hello --image=busybox --dry-run=client -o yaml -- echo hi > job.yaml

k delete job my-job
```

## Minimal YAML Example

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: pi
spec:
  completions: 3
  parallelism: 2
  backoffLimit: 4
  ttlSecondsAfterFinished: 60
  template:
    spec:
      restartPolicy: Never
      containers:
        - name: pi
          image: perl:5.34
          command: ["perl", "-Mbignum=bpi", "-wle", "print bpi(2000)"]
```
