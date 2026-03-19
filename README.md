# 🚀 Observability Stack using ArgoCD + Helm (GitOps)

This project deploys a full Kubernetes observability stack using **ArgoCD and Helm** following GitOps principles.

---

## 🧠 What This Project Does

It deploys:

* 📊 **Prometheus Stack (kube-prometheus-stack)**

  * Prometheus (metrics)
  * Alertmanager
  * Grafana (dashboards)

* 📜 **Loki**

  * Log aggregation backend

* 🚚 **Promtail**

  * Collects logs from nodes and sends to Loki

---

## ⚙️ Tech Stack

* Kubernetes
* ArgoCD (GitOps controller)
* Helm (package manager)
* Prometheus + Grafana + Loki

---

## 🏗️ Architecture

```
Git Repo
   ↓
ArgoCD
   ↓ (Helm templating)
Kubernetes Cluster
```

Each component is deployed as a **separate ArgoCD Application**.

---

## 📁 Repository Structure

```
observability-gitops/
├── apps/
│   ├── kube-prometheus/
│   ├── loki/
│   └── promtail/
└── root-app.yaml
```

---

## 🚀 Deployment

### Step 1: Update Repo URL

Edit `root-app.yaml`:

```
repoURL: https://github.com/YOUR_USERNAME/observability-gitops
```

---

### Step 2: Apply Root App

```
kubectl apply -f root-app.yaml
```

---

### Step 3: Watch ArgoCD

```
kubectl get applications -n argocd
```

---

## 🌐 Access Grafana

Port-forward:

```
kubectl port-forward svc/kube-prometheus-stack-grafana 3000:80 -n monitoring
```

Open:

```
http://localhost:3000
```

---

## 🔐 Credentials

* Username: `admin`
* Password: `admin` (change in values.yaml)

---

## ⚡ Key Design Decisions

* Helm charts used for all infra components
* ArgoCD manages deployments (GitOps)
* Grafana bundled with kube-prometheus-stack
* Loki + Promtail for logging

---

## 🧩 Why This Approach?

* Declarative infrastructure
* Easy upgrades (just change chart version)
* Self-healing via ArgoCD
* Clean separation of components

---

## 📈 Next Improvements

* Persistent volumes (important for production)
* Ingress + TLS
* Alerting rules
* Dashboard provisioning
* Secret management (SOPS / Sealed Secrets)

---

## 🙌 Summary

This repo demonstrates a **real-world GitOps observability setup** using:

* ArgoCD for deployment
* Helm for templating
* Kubernetes for runtime

---

Happy monitoring 🚀