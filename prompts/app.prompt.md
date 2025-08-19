Objective: Generate a Deployment and a ClusterIP Service for a simple web app.

Constraints:
- Name the Deployment and Service `go-demo-app`.
- Add labels: app=go-demo-app, tier=web.
- 2 replicas.
- Container `app` uses image `nginx:1.27.0`, exposes containerPort 8080.
- Service exposes port 80 -> targetPort 8080.
- Output as a multi-document YAML (---). Do not set a namespace.

Deliverable: Valid Kubernetes YAML for apps/v1 Deployment and v1 Service.
