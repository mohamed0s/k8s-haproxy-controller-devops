# 🧭 Kubernetes HAProxy Controller DevOps Setup

This repository documents the step-by-step setup of an HAProxy-based ingress controller on Kubernetes using Minikube.  
All manifests are stored under the **/manifests** directory, and screenshots under **/screenshots**.

---

## 🧱 Environment
- **Platform:** Red Hat 9.6  
- **Kubernetes:** v1.30.0 (via Minikube)  
- **Driver:** Docker  

---

## 🧩 Step 1 — Create Namespace

### 🎯 Goal
Create a dedicated namespace called **`haproxy-controller-devops`** to isolate all HAProxy ingress resources.

**Manifest:** [01-namespace.yaml](./manifests/01-namespace.yaml)

**Commands:**
```bash
kubectl apply -f manifests/01-namespace.yaml
kubectl get ns
```

📸 Screenshot:  
![Namespace Created](./screenshots/01-namespace-created.png)

---

## 🧩 Step 2 — Create ServiceAccount

### 🎯 Goal
Create a ServiceAccount named **`haproxy-service-account-devops`** under the same namespace (**`haproxy-controller-devops`**) that will be used by the HAProxy ingress controller to access cluster resources securely.

**Manifest:** [02-serviceaccount.yaml](./manifests/02-serviceaccount.yaml)

**Commands:**
```bash
kubectl apply -f manifests/02-serviceaccount.yaml
kubectl get sa -n haproxy-controller-devops
```

📸 Screenshot:  
![Service Account Created](./screenshots/02-serviceaccount-created.png)

---

## 🧱 Step 3 — Create ClusterRole

### 🎯 Goal
Create a ClusterRole named **`haproxy-cluster-role-devops`** that grants HAProxy permissions to interact with required Kubernetes objects (pods, services, configmaps, etc.).

**Manifest:** [03-clusterrole.yaml](./manifests/03-clusterrole.yaml)

**Commands:**
```bash
kubectl apply -f manifests/03-clusterrole.yaml
kubectl get clusterrole | grep haproxy
```

📸 Screenshot:  
![ClusterRole Created](./screenshots/03-clusterrole-created.png)

## 🧩 Step 4 — Create ClusterRoleBinding

### 🎯 Goal
Bind the **ClusterRole** `haproxy-cluster-role-devops` to the **ServiceAccount** `haproxy-service-account-devops` under the namespace **`haproxy-controller-devops`**.  
This allows the HAProxy controller to actually use the permissions defined in the ClusterRole.

**Manifest:** [04-clusterrolebinding.yaml](./manifests/04-clusterrolebinding.yaml)

**Commands:**
```bash
kubectl apply -f manifests/04-clusterrolebinding.yaml
kubectl get clusterrolebinding | grep haproxy
```

📸 Screenshot:  
![ClusterRoleBinding Created](./screenshots/04-clusterrolebinding-created.png)
