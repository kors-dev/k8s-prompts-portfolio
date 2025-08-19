Objective: Add a liveness probe to a web app Deployment.

Constraints:
- Deployment name: go-demo-app-liveness (apps/v1).
- Labels: app=go-demo-app, component=liveness.
- Image: nginx:1.27.0, containerPort 8080.
- HTTP livenessProbe on path /live, port 8080.
- initialDelaySeconds: 10, periodSeconds: 10, timeoutSeconds: 2, failureThreshold: 3.

Deliverable: Single Deployment YAML.
