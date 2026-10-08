# Docker & Kubernetes Containers

Containerizing a small Node.js web app with **Docker** and deploying it to **Kubernetes** — Deployment, NodePort Service, DaemonSet and persistent storage. Based on the IBM Skills Network `containers-project` template (Apache-2.0).

## The app

`main.js` is a dependency-free Node.js HTTP server that serves `public/index.html` on port **3000**.

## Build and run with Docker

```bash
docker build -t myapp:v1 .
docker run -p 3000:3000 myapp:v1
# open http://localhost:3000
```

## Deploy to Kubernetes

Push the image to your registry, set the `image:` field in the manifests (placeholder: `us.icr.io/<your SN labs namespace>/myapp:v1`), then:

```bash
kubectl apply -f k8s/deployment.yaml      # Deployment: 1 replica, rolling updates, CPU requests/limits
kubectl apply -f k8s/service.yaml         # NodePort Service exposing port 3000
kubectl apply -f k8s/daemonset.yaml       # DaemonSet: one pod per node
kubectl apply -f k8s/volume-and-pvc.yaml  # 1 Gi PersistentVolume + PersistentVolumeClaim
kubectl get pods,svc
```

## Project structure

```
├── Dockerfile          # node:14 image running main.js
├── main.js             # HTTP server
├── public/             # index.html, style.css
└── k8s/                # Kubernetes manifests
```

---
Author: Nguyen Quoc Anh — FPT University
