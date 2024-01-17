# ArgoCD Installation on Kubernetes using EC2 Instances

## Installation Steps

1. **Create ArgoCD Namespace:**

    ```bash
    kubectl create namespace argocd
    kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
    ```

2. **Access ArgoCD UI:**

    ```bash
    kubectl get svc -n argocd
    ```

3. **Port Forwarding for Access:**

    ```bash
    kubectl port-forward svc/argocd-server --address 0.0.0.0 8080:443 -n argocd
    ```

4. **Login to ArgoCD UI:**

    Use your web browser to navigate to `http://localhost:8080`. Login with the admin user and the token obtained from:

    ```bash
    kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo
    ```

5. **Avoid Timeouts (Optional):**

    To prevent timeouts, use the following command to keep the port forwarding active:

    ```bash
    while true; do kubectl port-forward svc/argocd-server --address 0.0.0.0 8080:443 -n argocd; done
    ```

## Notes

- Ensure you have a running Kubernetes cluster on EC2 instances.
- Customize commands as needed for your specific environment.
- Refer to [ArgoCD Documentation](https://argoproj.github.io/argo-cd/) for more details.

Feel free to customize this README according to your specific use case and add any additional information or context.
