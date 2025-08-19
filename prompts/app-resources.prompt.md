Objective: Set resource requests/limits for the app.

Constraints:
- Deployment name: go-demo-app-resources (apps/v1), 2 replicas.
- Image nginx:1.27.0, containerPort 8080.
- resources: requests cpu=100m, memory=128Mi; limits cpu=500m, memory=256Mi.

Deliverable: Deployment YAML with resources section filled.
