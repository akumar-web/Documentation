# 🚀 ArgoCD Best Practices

---

### ✅ I created ArgoCD in its own namespace
> Helps isolate ArgoCD components from other workloads for better control and security.

---

### 🔐 I Enable RBAC policies to restrict user permissions
> Apply fine-grained access control to users and service accounts using Role-Based Access Control.

---

### 🌐 I use Git repositories over HTTPS with deploy keys, not SSH
> Prevents potential SSH key mismanagement and simplifies secret rotation.

---

### 🔍 I can enable Audit logs and SSO for access control
> Enable single sign-on (SSO) integration and keep audit logs for all changes for accountability and visibility.

---

### 🔁 Will Rotate tokens regularly and avoid storing plaintext secrets
> Regularly rotate access tokens and credentials. Never store sensitive data in unencrypted form.

---
