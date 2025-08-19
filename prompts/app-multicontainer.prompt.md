Objective: Create a Pod with two containers sharing logs.

Constraints:
- Pod name: go-demo-app-mc (v1).
- Volume: emptyDir called `shared-logs` mounted at /var/log for both containers.
- Container `app` (busybox:1.36) appends to /var/log/app.log every 5s.
- Sidecar `log-tailer` (busybox:1.36) tails /var/log/app.log.

Deliverable: Single Pod YAML.
