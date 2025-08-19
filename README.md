# Kubernetes Prompt Portfolio (Generation + Examples)

> This repo showcases prompt-engineering for Kubernetes manifests that can be used with tools like [`kubectl-ai`](https://github.com/GoogleCloudPlatform/kubectl-ai).  
> Each row includes the **full prompt text**, description, and a link to the resulting YAML under [`/yaml`](./yaml).

## Generation Prompts

| NAME | PROMPT (full) | DESCRIPTION | EXAMPLE |
|---|---|---|---|
| app.yaml | ```
Objective: Generate a Deployment and a ClusterIP Service for a simple web app.

Constraints:
- Name the Deployment and Service `go-demo-app`.
- Add labels: app=go-demo-app, tier=web.
- 2 replicas.
- Container `app` uses image `nginx:1.27.0`, exposes containerPort 8080.
- Service exposes port 80 -> targetPort 8080.
- Output as a multi-document YAML (---). Do not set a namespace.

Deliverable: Valid Kubernetes YAML for apps/v1 Deployment and v1 Service.
``` | Base app + service (Deployment + ClusterIP). | [yaml/app.yaml](./yaml/app.yaml) |
| app-livenessProbe.yaml | ```
Objective: Add a liveness probe to a web app Deployment.

Constraints:
- Deployment name: go-demo-app-liveness (apps/v1).
- Labels: app=go-demo-app, component=liveness.
- Image: nginx:1.27.0, containerPort 8080.
- HTTP livenessProbe on path /live, port 8080.
- initialDelaySeconds: 10, periodSeconds: 10, timeoutSeconds: 2, failureThreshold: 3.

Deliverable: Single Deployment YAML.
``` | Crash detection & restart. | [yaml/app-livenessProbe.yaml](./yaml/app-livenessProbe.yaml) |
| app-readinessProbe.yaml | ```
Objective: Add a readiness probe to a web app Deployment.

Constraints:
- Deployment name: go-demo-app-readiness (apps/v1).
- Labels: app=go-demo-app, component=readiness.
- Image: nginx:1.27.0, containerPort 8080.
- HTTP readinessProbe on path /ready, port 8080.
- initialDelaySeconds: 5, periodSeconds: 10, timeoutSeconds: 2, failureThreshold: 3.

Deliverable: Single Deployment YAML.
``` | Traffic gating until ready. | [yaml/app-readinessProbe.yaml](./yaml/app-readinessProbe.yaml) |
| app-volumeMounts.yaml | ```
Objective: Mount persistent storage into the app container.

Constraints:
- Deployment name: go-demo-app-storage (apps/v1).
- Labels: app=go-demo-app, component=storage.
- Container image: nginx:1.27.0 with containerPort 8080.
- Mount a volume named `app-data` at `/data`.
- Provide a matching PersistentVolumeClaim named `app-data` requesting 1Gi, RWO.
- Output both Deployment and PVC in a multi-doc YAML.

Deliverable: Deployment + PVC YAML.
``` | Persistent storage example. | [yaml/app-volumeMounts.yaml](./yaml/app-volumeMounts.yaml) |
| app-cronjob.yaml | ```
Objective: Create a nightly backup CronJob.

Constraints:
- Name: db-backup (batch/v1).
- Schedule: 0 3 * * *.
- Use busybox:1.36 to simulate backup: `sh -c 'echo $(date) backup started && sleep 10 && echo done'`.
- concurrencyPolicy: Forbid; startingDeadlineSeconds: 120.
- Set restartPolicy: OnFailure; keep a small history.

Deliverable: CronJob YAML.
``` | Scheduled task pattern. | [yaml/app-cronjob.yaml](./yaml/app-cronjob.yaml) |
| app-job.yaml | ```
Objective: Create a one-off migration Job.

Constraints:
- Name: one-off-migration (batch/v1).
- Container image: busybox:1.36.
- Command: `sh -c 'echo running db migration && sleep 5 && echo ok'`.
- restartPolicy: Never; backoffLimit: 1.

Deliverable: Job YAML.
``` | Batch task example. | [yaml/app-job.yaml](./yaml/app-job.yaml) |
| app-multicontainer.yaml | ```
Objective: Create a Pod with two containers sharing logs.

Constraints:
- Pod name: go-demo-app-mc (v1).
- Volume: emptyDir called `shared-logs` mounted at /var/log for both containers.
- Container `app` (busybox:1.36) appends to /var/log/app.log every 5s.
- Sidecar `log-tailer` (busybox:1.36) tails /var/log/app.log.

Deliverable: Single Pod YAML.
``` | Sidecar logging pattern. | [yaml/app-multicontainer.yaml](./yaml/app-multicontainer.yaml) |
| app-resources.yaml | ```
Objective: Set resource requests/limits for the app.

Constraints:
- Deployment name: go-demo-app-resources (apps/v1), 2 replicas.
- Image nginx:1.27.0, containerPort 8080.
- resources: requests cpu=100m, memory=128Mi; limits cpu=500m, memory=256Mi.

Deliverable: Deployment YAML with resources section filled.
``` | Resource governance. | [yaml/app-resources.yaml](./yaml/app-resources.yaml) |
| app-secret-env.yaml | ```
Objective: Inject configuration via Secret as environment variables.

Constraints:
- Create a Secret `app-secret` (type Opaque) with keys DB_URL and API_KEY (base64 values are fine).
- Create a Deployment `go-demo-app-secret` whose container uses envFrom.secretRef to load that secret.
- Image nginx:1.27.0, containerPort 8080.
- Output: Secret and Deployment as a multi-doc YAML.

Deliverable: Secret + Deployment YAML.
``` | Config via Secret env. | [yaml/app-secret-env.yaml](./yaml/app-secret-env.yaml) |

## Bonus: Analysis Prompts

- [`prompts/analysis-security.prompt.md`](./prompts/analysis-security.prompt.md) — security & reliability review checklist.  
- [`prompts/analysis-ops.prompt.md`](./prompts/analysis-ops.prompt.md) — operability (HPA/PDB/rollout) improvements.

## How to Use with `kubectl-ai`

1. Install the plugin (see official repo).  
2. Copy a prompt from `/prompts/*.prompt.md` and run, for example:  
   ```bash
   kubectl ai generate -f - <<'EOF'
   <paste prompt here>
   EOF
   ```
3. Compare with the example manifest in `/yaml`.

---

### Marketing Summary
- Automated Kubernetes YAML generation via reproducible, testable prompts (generation + analysis tracks).
- Patterns included: health probes, storage, jobs/cron, sidecars, resource governance, and secret-driven configuration.
- Works with Google Cloud’s `kubectl-ai`; prompts are constraint-driven, review-ready, and showcase DevOps automation practice.

---
