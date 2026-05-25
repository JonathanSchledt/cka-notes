# CronJobs

## Concept

Schedules Jobs on a cron expression

Schedule format: `minute hour day-of-month month day-of-week`

Fields:

- schedule: cron expression
- successfulJobsHistoryLimit (default 3)
- failedJobsHistoryLimit (default 1)
- concurrencyPolicy: Allow (default), Forbid, Replace
- suspend: pause without deleting

## Key Commands

```bash
k get cj

k get jobs --watch

# generate yaml
k create cronjob hello --image=busybox --schedule="*/1 * * * *" \
  --dry-run=client -o yaml -- echo hi > cj.yaml

# trigger a CronJob manually
k create job --from=cronjob/hello hello-manual

# suspend / resume
k patch cronjob hello -p '{"spec":{"suspend":true}}'
```

## Minimal YAML Example

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: hello
spec:
  schedule: "*/1 * * * *"
  concurrencyPolicy: Forbid
  successfulJobsHistoryLimit: 3
  failedJobsHistoryLimit: 1
  jobTemplate:
    spec:
      template:
        spec:
          restartPolicy: OnFailure
          containers:
            - name: hello
              image: busybox
              command: ["sh", "-c", "date; echo hello"]
```
