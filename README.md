# taskflow-gitops

GitOps configuration repository for the Taskflow application, managed by ArgoCD on Kubernetes.

## Structure

```
.
├── argocd/          # ArgoCD Application manifests
│   ├── frontend-app.yaml
│   └── backend-app.yaml
├── frontend/        # Frontend Kubernetes manifests
│   ├── deployment.yaml
│   └── service.yaml
└── backend/         # Backend Kubernetes manifests
    ├── deployment.yaml
    └── service.yaml
```

## How it works

ArgoCD watches this repository and automatically syncs changes to the cluster. Both the frontend and backend apps have `automated` sync enabled with `prune` and `selfHeal` turned on.

## Secrets

The backend deployment expects a `taskflow-secret` Kubernetes Secret with the following keys:

- `DATABASE_URL` — PostgreSQL connection string
- `JWT_SECRET` — Secret used to sign JWT tokens

An `ecr-secret` is also required for pulling images from AWS ECR.
