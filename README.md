
# Install Jenkins on Google Kubernetes Engine (GKE) using Helm

## Prerequisites
- Google Cloud SDK installed and configured
- Helm installed (version >= 3.x)
- kubectl installed and configured to interact with your GKE cluster

## Steps

### 1. Add Jenkins Helm repository
```bash
helm repo add jenkins https://charts.jenkins.io
helm repo update
kubectl create namespace jenkins
