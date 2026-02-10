# Web_Application_Over_Kubernetes_Cluster_GCP


This project demonstrates deploying a **Flask web application** with a **MongoDB Database** on Kubernetes using:

- Deployments
- Services
- Persistent Volumes
- Persistent Volume Claims

It provisions a scalable web tier connected to a stateful database with persistent storage.

---

## Project Structure

```
.
├── webserver-deploy.yaml     # Flask webserver Deployment
├── serviceWEB.yaml           # NodePort Service for web access
├── mongodb-deploy.yaml       # MongoDB Deployment
├── DBService.yaml            # MongoDB ClusterIP Service
├── mongopersistent.yaml      # Persistent Volume + PVC
```

---

## Architecture Overview

- **Flask Web Server**
  - 3 replicas
  - Exposed via NodePort
  - Connects to MongoDB Database

- **MongoDB**
  - Single replica
  - Persistent storage mounted
  - Internal ClusterIP service

- **Storage**
  - HostPath Persistent Volume
  - PVC bound to MongoDB pod

---

## Deployment Steps

### 1️⃣ Create Persistent Storage

```bash
kubectl apply -f mongopersistent.yaml
```

### 2️⃣ Deploy MongoDB

```bash
kubectl apply -f mongodb-deploy.yaml
kubectl apply -f DBService.yaml
```

### 3️⃣ Deploy Web Application

```bash
kubectl apply -f webserver-deploy.yaml
kubectl apply -f serviceWEB.yaml
```

---

## Verify Resources

```bash
kubectl get pods
kubectl get services
kubectl get pvc
kubectl get pv
```

---

## Access the Application

Get node IP:

```bash
kubectl get nodes -o wide
```

Access using:

```
http://<NODE-IP>:31100
```

---

## 🛠 Technologies Used

- Kubernetes
- Docker
- Flask
- MongoDB

---

## Notes

- Ensure Kubernetes cluster has permission to use `hostPath`.
- Replace container images if deploying to cloud registry.
- Secrets should be stored in Kubernetes Secrets for production use.

---
