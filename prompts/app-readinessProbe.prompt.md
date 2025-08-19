Objective: Add a readiness probe to a web app Deployment.

Constraints:
- Deployment name: go-demo-app-readiness (apps/v1).
- Labels: app=go-demo-app, component=readiness.
- Image: nginx:1.27.0, containerPort 8080.
- HTTP readinessProbe on path /ready, port 8080.
- initialDelaySeconds: 5, periodSeconds: 10, timeoutSeconds: 2, failureThreshold: 3.

Deliverable: Single Deployment YAML.
