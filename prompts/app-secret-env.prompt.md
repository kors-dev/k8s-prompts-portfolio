Objective: Inject configuration via Secret as environment variables.

Constraints:
- Create a Secret `app-secret` (type Opaque) with keys DB_URL and API_KEY (base64 values are fine).
- Create a Deployment `go-demo-app-secret` whose container uses envFrom.secretRef to load that secret.
- Image nginx:1.27.0, containerPort 8080.
- Output: Secret and Deployment as a multi-doc YAML.

Deliverable: Secret + Deployment YAML.
