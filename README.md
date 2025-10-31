
## 🏗️ Pipeline Stages (high level)
1. **Checkout** source from GitHub  
2. **Build** Docker image  
3. **SonarQube** analysis (quality gate)  
4. **Trivy** image scan (fail on high/critical)  
5. **Push** image to Docker Hub (e.g., `abkaur95/webapp:<buildNumber>`)  
6. **Bump image tag** in the **manifests repo** (`ci-cd-k8s-manifests/k8s/deployment.yaml`) and push a commit  
7. **Argo CD** detects the manifest change and deploys to the cluster

## 🔗 Linked Repositories
- **Manifests repo (GitOps):** https://github.com/abkaur/ci-cd-k8s-manifests

## 🔐 Required Jenkins credentials (examples)
- `dockerhub-creds` – Docker Hub username/password (or token)
- `git-manifests-creds` – PAT/SSH key to push to manifests repo
- `sonarqube-server` – Jenkins global config for SonarQube server URL/token

## ⚙️ Environment Variables (examples)
- `DOCKER_IMAGE=abkaur95/webapp`
- `MANIFESTS_REPO=https://github.com/abkaur/ci-cd-k8s-manifests.git`
- `MANIFESTS_PATH=k8s/deployment.yaml`

## 🧪 Local run (optional)
```bash
docker build -t webapp:local .
docker run -p 8010:8010 webapp:local
# open http://localhost:8010

