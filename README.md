# 📦 GitOps Manifests for CI/CD Deployment (Argo CD)

This repository holds the **Kubernetes manifests** for the Python web app.  
It is updated **automatically by Jenkins** (image tag bump), and **Argo CD** watches this repo to sync the desired state to the cluster.

## 🔗 Related App Repository
- App + pipeline: https://github.com/abkaur/ci-cd-python-webapp

## 📂 Structure
k8s/
deployment.yaml # image: abkaur95/webapp:<TAG> ← Jenkins updates this tag
service.yaml
README.md

## 🔁 How Updates Happen
1. Jenkins builds & scans the app image (in the app repo).
2. Jenkins **bumps the `image: ...:<tag>`** in `k8s/deployment.yaml` here and pushes a commit (e.g., “Updated image tag to 11”).
3. **Argo CD** detects the commit and **syncs** the new image version to the Kubernetes cluster.

## 🧭 Argo CD Setup (high level)
- Application source: this repo (path: `k8s/`)
- Destination: your K8s cluster/namespace
- Sync policy: Manual or **Auto-Sync** (recommended for continuous delivery)

## 🔐 Notes
- The manifests are intentionally simple (plain YAML).  
  You can evolve this into a **Helm chart** later for values management and multi-env support.
- Ensure your Argo CD app has read access to this repository.

## 🧠 What I Practiced / Learned
- The **separation of concerns**: app build repo vs. deployment manifests repo
- **GitOps** with Argo CD (Git as the source of truth)
- Safe, traceable deployments via **commit history** (e.g., “Updated image tag to 11”)


"For screenshots of Argo CD sync and cluster output, see the April 27 Task Report in the app repository docs folder"
