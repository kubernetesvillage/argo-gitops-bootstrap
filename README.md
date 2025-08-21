# Argo CD GitOps Demo

This repository demonstrates a minimal **GitOps deployment using Argo CD**, following the app-of-apps pattern. It bootstraps Argo CD and deploys a sample Helm-based application `stefanprodan/podinfo`.

## Structure

```
.
├── bootstrap/
│   ├── kustomization.yaml             # Kustomize entrypoint to install Argo CD and root Application
│   ├── argocd-bootstrap-app.yaml     # Root Argo CD Application (app-of-apps pattern)
│   └── podinfo-demo-app.yaml         # Sample Helm-based Application (podinfo)
└── README.md
```

## Flow

1. Argo CD is installed via upstream pinned manifests.
2. A root application (`argocd-bootstrap-app`) deploys all child applications.
3. `podinfo` is deployed via Helm chart using Argo CD.

## Deployment Commands

```bash
# Create folder structure
mkdir -p bootstrap
```

```bash
# Apply Argo CD installation and root app via Kustomize
kubectl apply -k bootstrap/

# Wait for Argo CD to be ready (optional but recommended)
kubectl -n argocd rollout status deploy/argocd-server
kubectl -n argocd rollout status deploy/argocd-repo-server
kubectl -n argocd rollout status deploy/argocd-application-controller
```



## Reference:
- [Chatgpt 4o](https://chatgpt.com)
- [NiniiGit](https://github.com/NiniiGit/argocd-demo)
- [cloudyuga.guru](https://cloudyuga.guru/blogs/gitops-argocd-fluxcd/)