# Kubernetes Prompt Portfolio (Generation + Examples)

> This repo showcases prompt-engineering for Kubernetes manifests that can be used with tools like [`kubectl-ai`](https://github.com/GoogleCloudPlatform/kubectl-ai). Each row includes a concise prompt, what it does, and a link to the resulting YAML under [`/yaml`](./yaml).

## Generation Prompts

| NAME                | PROMPT                                                                                         | DESCRIPTION                                    | EXAMPLE                           |
|---------------------|------------------------------------------------------------------------------------------------|------------------------------------------------|-----------------------------------|
| Secret Env          | Generate a Kubernetes Secret manifest with environment variables for my app                    | Create a Secret resource to store environment variables | [app-secret-env.yaml](./yaml/app-secret-env.yaml) |
| Volume Mounts       | Create a Deployment manifest with volume mounts for persistent data                            | Define volume mounts in a Pod to persist data   | [app-volumeMounts.yaml](./yaml/app-volumeMounts.yaml) |
| Basic Deployment    | Generate a simple Kubernetes Deployment manifest for an app with port 8080                     | A basic Deployment exposing port 8080           | [app.yaml](./yaml/app.yaml) |
| CronJob             | Generate a Kubernetes CronJob manifest that runs every day at midnight                         | Automate task execution on a schedule           | [app-cronjob.yaml](./yaml/app-cronjob.yaml) |
| Job                 | Generate a Kubernetes Job manifest that runs a script once                                     | One-time task execution using a Job resource    | [app-job.yaml](./yaml/app-job.yaml) |
| Liveness Probe      | Add a livenessProbe to a container checking /healthy on port 8080                              | Health check to restart containers when needed  | [app-livenessProbe.yaml](./yaml/app-livenessProbe.yaml) |
| Multi-Container Pod | Create a Kubernetes Pod with two containers sharing a volume                                   | Define a Pod with multiple containers sharing a volume | [app-multicontainer.yaml](./yaml/app-multicontainer.yaml) |
| Readiness Probe     | Add a readinessProbe checking /ready on port 8080                                              | Check container readiness before serving traffic | [app-readinessProbe.yaml](./yaml/app-readinessProbe.yaml) |
| Resources           | Add resource requests and limits for CPU and memory to a container                             | Control CPU and memory resource allocation      | [app-resources.yaml](./yaml/app-resources.yaml) |

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
