# Bootstrap ArgoCD GitOps

This directory contains the bootstrap configuration for ArgoCD GitOps setup.

## Initial Setup

1. **Install ArgoCD** (if not already installed):
   ```bash
   kubectl create namespace argocd
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```

2. **Create the ArgoCD Project**:
   ```bash
   kubectl apply -f bootstrap/argocd-project.yaml
   ```

3. **Deploy the Root App** (App of Apps pattern):
   ```bash
   kubectl apply -f bootstrap/root-app.yaml
   ```

## How It Works

- **argocd-project.yaml**: Defines the `homelab` project with permissions
- **root-app.yaml**: Root Application that monitors the `apps/` directory
- The root app automatically deploys ApplicationSets from `apps/`
- ApplicationSets discover and deploy apps from their respective directories

## Structure

```
k8s-argocd-gitops/
├── bootstrap/           # Bootstrap ArgoCD (this directory)
├── apps/               # ApplicationSets that manage groups of apps
├── infrastructure/     # Infrastructure components (Helm charts)
├── applications/       # User applications
└── observability/      # Monitoring and logging
```

## Adding New Components

To add a new infrastructure component:

1. Create a directory: `infrastructure/my-component/`
2. Add an `app.yaml` file with your Helm chart or Git source configuration
3. Commit and push - ArgoCD will automatically deploy it!

## Accessing ArgoCD UI

```bash
# Get admin password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

# Port forward to access UI
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Then visit: https://localhost:8080
