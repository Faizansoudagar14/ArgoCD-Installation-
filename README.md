markdown
Copy code
# ArgoCD Installation on Kubernetes using EC2 Instances

This guide walks you through the installation of ArgoCD on a Kubernetes cluster using EC2 instances. ArgoCD is a declarative, GitOps continuous delivery tool for Kubernetes.

## Prerequisites

- Kubernetes cluster running on EC2 instances.
- kubectl installed locally.
- GitOps repository containing Kubernetes manifests.

## Installation Steps

1. **Create ArgoCD Namespace:**

   ```bash
   kubectl create namespace argocd
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
Access ArgoCD UI:

bash
Copy code
kubectl get svc -n argocd
Port Forwarding for Access:

bash
Copy code
kubectl port-forward svc/argocd-server --address 0.0.0.0 8080:443 -n argocd
Login to ArgoCD UI:

Open your web browser and navigate to http://localhost:8080. Login using the admin user and the token retrieved from:

bash
Copy code
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo
Avoid Timeouts (Optional):

If you face timeout issues, use the following command to keep the port forwarding active:

bash
Copy code
while true; do kubectl port-forward svc/argocd-server --address 0.0.0.0 8080:443 -n argocd; done
Customization
Modify the commands and values according to your specific Kubernetes setup.
Ensure that your GitOps repository is correctly configured with the desired manifests.
References
ArgoCD GitHub Repository
ArgoCD Documentation
