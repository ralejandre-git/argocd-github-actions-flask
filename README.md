### Deploy Python Flask App on Kubernetes cluster with GitOps Approach. 

## Test Application Locally. 
Whenever we are creating pipeline, it is best practice to test application locally.
- Application prequisities. 
  - Python 3.9 
  - pip installed

- Clone/Fork the Repo. 
    ```
    git clone https://github.com/infosecsingh/Flask-App-GitHub-Actions-ArgoCD.git
    cd Flask-App-GitHub-Actions-ArgoCD
    ```
- Install Dependence
    ```
    pip install -r requirements.txt
    ```
- Run locally. 
    ```
    python app.py
    ```
- Access the application.
    ```
    http://localhost:5000
    ```
---
## Containerize Application.

#### Build and Run the Container
1. Build the Image
2. Create container with image.
 
## CI Pipeline with GitHub Actions
1. Create a directory inside your project.
    ```
    mkdir -p .github/Workflows
    ```
2. Create your first pipeline for TEST and BUILD the image

3. Setup your docker Personal Access token into github repo. 

## Setup ArgoCD in Minikube

- First install Minikube:
    [Minikube.sigs.k8s.io](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download)

---
- Install Argo CD
    ```
    kubectl create namespace argocd
    kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml 
    ```

- Verify if ArgoCD is running:
    ```
    kubectl get all -n argocd
    ```
---
- Access ArgoCD With configuring NodePort 
    ```
    kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
    ```
- Verify if ArgoCD server running as NodePort.
   ```
   kubectl get svc -n argocd
   ``` 
- Grab ArgoCD secret for accessing UI
   ```
   kubectl get secrets -n argocd argocd-initial-admin-secret -o jsonpath='{.data.password}' | base64 -d
   ```
- Start Minkube Service. 
   ```
    minikube service argocd-server -n argocd
    ```
---
Setup CD pipeline in ArgoCD UI. 
---
Access Application with below command.
```
minikube service list
```
