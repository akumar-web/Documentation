# 🚀 Argo CD on Amazon EKS

This guide provides a quick and practical walkthrough to install **Argo CD** on an **Amazon EKS** cluster using the official [Argo CD Getting Started Guide](https://argo-cd.readthedocs.io/en/stable/getting_started/).

---

## ✅ Prerequisites

Make sure you have the following:

- An Amazon EKS cluster set up and `kubectl` configured
- `argocd` CLI installed (optional but useful)
- Access to the terminal or AWS CloudShell

---

## 📦 Step : Install Argo CD

```bash
kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Step 2: Access Argo CD UI & Log In
 #Expose Argo CD via LoadBalancer

kubectl patch svc argocd-server -n argocd \
  -p '{"spec": {"type": "LoadBalancer"}}'

kubectl get svc argocd-server -n argocd

# 🔐 Log in to Argo CD
#     Get the initial admin password:

kubectl get secret argocd-initial-admin-secret -n argocd \
  -o jsonpath="{.data.password}" | base64 -d && echo




