# k3s-arda

This repository contains the Kubernetes (K3s) configurations for deploying my self-hosted applications using ArgoCD. The structure follows a clear separation of concerns, ensuring easy management and scalability.

## Repository Structure

```
/k3s-arda
│── /infra
│   ├── /nfs-provisioner
│   │   ├── deployment.yaml
│   │   ├── storageclass.yaml
│   │   ├── kustomization.yaml
│   │   ├── nfs-provisioner-rolebinding.yaml
│   │   ├── nfs-service-account.yaml
│   │   ├── namespace.yaml
│   │   ├── nfs-provisioner-rbac.yaml
│── /argocd
│   ├── one-app.yaml
│   ├── another-app.yaml
│   ├── app-of-apps.yaml
│── /apps
│   ├── /one-app
│   │   ├── deployment.yaml
│   │   ├── a-pv.yaml
│   │   ├── kustomization.yaml
│   │   ├── another-pv.yaml
│   │   ├── app-ingress.yaml

```

### **1. `/infra/` - Infrastructure Components**
This directory houses infrastructure-related Kubernetes resources.
- **`nfs-provisioner/`**: Contains all configurations for setting up the NFS storage provisioner.
  - `deployment.yaml`: Deploys the NFS provisioner.
  - `storageclass.yaml`: Defines the default **StorageClass** using NFS.
  - `kustomization.yaml`: Allows resource management via Kustomize.
  - `namespace.yaml`: Defines the namespace for the provisioner.
  - `nfs-provisioner-rolebinding.yaml`, `nfs-provisioner-rbac.yaml`, `nfs-service-account.yaml`: Handles access control.

### **2. `/argocd/` - ArgoCD Applications**
Contains the definitions for deploying applications via ArgoCD.
- Each YAML file represents an ArgoCD **Application** that manages the deployment of a service.
- `app-of-apps.yaml`: The **root application**, which deploys all other applications.

### **3. `/apps/` - Application Deployments**
Each application has its own directory containing:
- **`deployment.yaml`**: Defines the app’s pod and resource specifications.
- **`ingress.yaml`**: Configures external access via Ingress (if applicable).
- **`pv.yaml` / `pvc.yaml`**: Defines persistent storage volumes (if needed).
- **`kustomization.yaml`**: Allows for Kubernetes-native templating using Kustomize.

## Deployment Workflow
1. Push changes to this repository.
2. ArgoCD detects changes and applies updates automatically.
3. Kubernetes resources are deployed and managed within the cluster.

---
This setup ensures a **scalable, declarative, and GitOps-based** approach to managing K3s deployments. 🚀

