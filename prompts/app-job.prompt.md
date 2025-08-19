Objective: Create a one-off migration Job.

Constraints:
- Name: one-off-migration (batch/v1).
- Container image: busybox:1.36.
- Command: `sh -c 'echo running db migration && sleep 5 && echo ok'`.
- restartPolicy: Never; backoffLimit: 1.

Deliverable: Job YAML.
