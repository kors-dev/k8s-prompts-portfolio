Objective: Mount persistent storage into the app container.

Constraints:
- Deployment name: go-demo-app-storage (apps/v1).
- Labels: app=go-demo-app, component=storage.
- Container image: nginx:1.27.0 with containerPort 8080.
- Mount a volume named `app-data` at `/data`.
- Provide a matching PersistentVolumeClaim named `app-data` requesting 1Gi, RWO.
- Output both Deployment and PVC in a multi-doc YAML.

Deliverable: Deployment + PVC YAML.
