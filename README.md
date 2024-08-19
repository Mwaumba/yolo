# GKE Autopilot Cluster Deployment
This project involves deploying a Kubernetes application on Google Kubernetes Engine (GKE) using Autopilot mode.
2. **Build and Tag Docker Images**:
   Build the Docker image:
   ```bash
   docker build -t my-app:latest .
   ## Kubernetes Manifests

- **Deployments:**
  - Located in `k8s/deployments/`

- **StatefulSets:**
  - Located in `k8s/statefulsets/`

- **Services:**
  - Located in `k8s/services/`

- **PersistentVolumeClaims:**
  - Located in `k8s/persistent-volumes/`
  ## Access Instructions

Access the frontend application using the LoadBalancer IP or URL provided by the `frontend-service`.

