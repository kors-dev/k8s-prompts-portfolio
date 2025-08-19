# Kubernetes Prompt Portfolio (Generation + Examples)

> This repo showcases prompt-engineering for Kubernetes manifests that can be used with tools like [`kubectl-ai`](https://github.com/GoogleCloudPlatform/kubectl-ai). Each row includes a concise prompt, what it does, and a link to the resulting YAML under [`/yaml`](./yaml).

## Generation Prompts

| NAME | PROMPT (concise) | DESCRIPTION | EXAMPLE |
|---|---|---|---|
| app.yaml | Generate Deployment `go-demo-app` (2 replicas, nginx:1.27.0 on 8080) + ClusterIP Service (80→8080). | Base app + service. | [yaml/app.yaml](./yaml/app.yaml) |
| app-livenessProbe.yaml | Add HTTP livenessProbe on `/live` (10s delay/period) to Deployment `go-demo-app-liveness`. | Crash detection & restart. | [yaml/app-livenessProbe.yaml](./yaml/app-livenessProbe.yaml) |
| app-readinessProbe.yaml | Add HTTP readinessProbe on `/ready` (5s delay) to Deployment `go-demo-app-readiness`. | Traffic gating until ready. | [yaml/app-readinessProbe.yaml](./yaml/app-readinessProbe.yaml) |
| app-volumeMounts.yaml | Mount PVC `app-data` at `/data` in Deployment `go-demo-app-storage`; include PVC 1Gi RWO. | Persistent storage example. | [yaml/app-volumeMounts.yaml](./yaml/app-volumeMounts.yaml) |
| app-cronjob.yaml | Nightly CronJob `db-backup` at `0 3 * * *` using busybox; forbid concurrency. | Scheduled task pattern. | [yaml/app-cronjob.yaml](./yaml/app-cronjob.yaml) |
| app-job.yaml | One-off Job `one-off-migration` using busybox; restartPolicy Never; backoffLimit 1. | Batch task example. | [yaml/app-job.yaml](./yaml/app-job.yaml) |
| app-multicontainer.yaml | Pod with `app` + `log-tailer` sharing `emptyDir` at /var/log; tail file. | Sidecar logging pattern. | [yaml/app-multicontainer.yaml](./yaml/app-multicontainer.yaml) |
| app-resources.yaml | Deployment with requests: 100m/128Mi, limits: 500m/256Mi. | Resource governance. | [yaml/app-resources.yaml](./yaml/app-resources.yaml) |
| app-secret-env.yaml | Secret `app-secret` + Deployment consuming via `envFrom.secretRef`. | Config via Secret env. | [yaml/app-secret-env.yaml](./yaml/app-secret-env.yaml) |

Full prompts live under [`/prompts`](./prompts).

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

### Marketing Summary (short)
- Automated Kubernetes YAML generation via reproducible, testable prompts (generation + analysis tracks).
- Patterns included: health probes, storage, jobs/cron, sidecars, resource governance, and secret-driven configuration.
- Works with Google Cloud’s `kubectl-ai`; prompts are concise, constraint-driven, and review-ready.

---

> Source reference app manifests: inspired by common patterns seen in demo apps like [`go-demo-app`](https://github.com/den-vasyliev/go-demo-app).
