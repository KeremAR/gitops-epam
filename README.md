### GitOps Structure: App of Apps

We use the "App of Apps" pattern to structure our GitOps repository. This provides a centralized and scalable way to manage multiple applications and environments.

- **`root-application.yaml`**: This is the parent application. It is configured to monitor a path in the GitOps repository (e.g., `environments/`) and automatically create any `Application` resources defined there. This allows for easy onboarding of new environments or applications.

- **Environment Applications (`staging.yaml`, `production.yaml`)**: These are child applications managed by the root application. Each file defines the deployment for a specific environment:
    - They point to the `todo-app` Helm chart.
    - They specify the target namespace (`staging` or `production`).
    - They provide environment-specific configurations using different Helm value files (`values-staging.yaml` or `values-prod.yaml`).
    - They are configured with an automated sync policy, ensuring that any changes merged to the main branch of the GitOps repository are automatically applied to the cluster.

**Note:** The GitOps manifests are maintained in a separate, dedicated Git repository.
