
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

### 2. Create a namespace for Jenkins
```bash
kubectl create namespace jenkins

### 3.helm install jenkins -n jenkins jenkins/jenkins

```bash
helm install jenkins -n jenkins jenkins/jenkins

### 4. Retrieve Jenkins admin password
```bash
kubectl exec -n jenkins $(kubectl get pods --namespace jenkins -l "app.kubernetes.io/component=jenkins-controller" -o jsonpath="{.items[0].metadata.name}") -- cat /var/jenkins_home/secrets/initialAdminPassword

### 5. Access Jenkins DashBoard
```bash
export SERVICE_IP=$(kubectl get svc --namespace jenkins jenkins -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
echo http://$SERVICE_IP:8080/login

6. Log in to Jenkins
Open the URL printed in the previous step in your web browser.
Enter the administrator password retrieved in step 4.
Follow the on-screen instructions to complete the setup.

### 7. Clean up optional
```bash
helm uninstall jenkins -n jenkins
kubectl delete namespace jenkins




