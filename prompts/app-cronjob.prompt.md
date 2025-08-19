Objective: Create a nightly backup CronJob.

Constraints:
- Name: db-backup (batch/v1).
- Schedule: 0 3 * * *.
- Use busybox:1.36 to simulate backup: `sh -c 'echo $(date) backup started && sleep 10 && echo done'`.
- concurrencyPolicy: Forbid; startingDeadlineSeconds: 120.
- Set restartPolicy: OnFailure; keep a small history.

Deliverable: CronJob YAML.
