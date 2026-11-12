# azure-boutique-aks

Google's Online Boutique (11 microservices) running on Azure Kubernetes Service, with a GitHub Actions pipeline that builds two of the services, pushes them to Azure Container Registry and rolls them out to AKS with automatic rollback.

This README is a work in progress; the full write-up (architecture, problems and fixes, screenshots) is added once the project is complete.

## Repository layout

| Path | Contents |
|---|---|
| `frontend/`, `cartservice/` | Source of the two services the pipeline builds (from Online Boutique) |
| `k8s/namespace.yaml` | `boutique` namespace |
| `k8s/kubernetes-manifests.yaml` | All 11 services; frontend and cartservice images point to ACR, CPU requests lowered to 10m to fit one 2-vCPU node, loadgenerator at 0 replicas |
| `.github/workflows/deploy.yml` | Build, push to ACR, deploy to AKS with rollback; Azure login via OIDC (no stored secret) |
| `docs/screenshots/` | Build-log screenshots |

## Credits

Application code and base manifests: [Online Boutique](https://github.com/GoogleCloudPlatform/microservices-demo) by Google, Apache License 2.0 (see `LICENSE`). Azure infrastructure, manifest changes and the pipeline are my own work.
