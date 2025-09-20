# End-to-End Project Manifests

This repository contains Kubernetes manifests for the End-to-End Python Flask Application. It's designed to work with ArgoCD for GitOps-based continuous deployment.

## 📁 Repository Structure

```
EndtoEnd-Project-Manifests/
├── mainfest/                     # Kubernetes manifests
│   ├── namespace.yaml           # Namespace configuration
│   ├── configmap.yaml           # Application configuration
│   ├── pv.yaml                  # Persistent Volume
│   ├── pvc.yaml                 # Persistent Volume Claim
│   ├── deployment.yaml          # Application deployment
│   ├── service.yaml             # Service configuration
│   ├── ingress.yaml             # Ingress configuration
│   └── kustomization.yaml       # Kustomize configuration
├── argocd/                       # ArgoCD application configurations
│   ├── application-dev.yaml     # Development environment
│   ├── application-staging.yaml # Staging environment
│   ├── application-prod.yaml    # Production environment
│   ├── install-argocd.sh        # ArgoCD installation script
│   └── setup-applications.sh    # Application setup script
└── README.md                     # This file
```

## 🚀 GitOps Workflow

1. **Jenkins Pipeline** builds Docker image and pushes to registry
2. **Jenkins** updates image tags in this repository
3. **ArgoCD** detects changes and automatically deploys to Kubernetes
4. **Application** is deployed to the target environment

## 🔧 Setup Instructions

### 1. Install ArgoCD
```bash
./argocd/install-argocd.sh
```

### 2. Create ArgoCD Applications
```bash
./argocd/setup-applications.sh
```

### 3. Access ArgoCD UI
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
# Open: https://localhost:8080
```

## 📊 Environments

- **Development**: `flask-app-dev` namespace
- **Staging**: `flask-app-staging` namespace  
- **Production**: `flask-app-prod` namespace

## 🔄 Automatic Deployment

This repository is monitored by ArgoCD. Any changes pushed to this repository will automatically trigger deployments to the corresponding Kubernetes environments.

## 📝 Notes

- Image tags are updated by Jenkins pipeline
- Each environment has its own ArgoCD application
- ArgoCD applications are configured for automatic sync
- All deployments are tracked and auditable through Git history
