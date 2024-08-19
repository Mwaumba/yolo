1. Choice of Base Images for Each Container
Frontend: node:14

Chosen for its stability and compatibility with the frontend application, which is built using Node.js version 14.
Backend: node:14

Same as the frontend, this image ensures consistency across development and production environments for the Node.js backend.
Database: mongo:4.4

The MongoDB image version 4.4 is selected for its compatibility with the application's requirements and its support for necessary MongoDB features.
2. Dockerfile Directives Used
Frontend and Backend Dockerfile:

FROM node:14: Uses Node.js version 14 as the base image.
WORKDIR /usr/src/app: Sets the working directory inside the container.
COPY package*.json ./: Copies package files for npm installation.
RUN npm install: Installs dependencies specified in package.json.
COPY . .: Copies the rest of the application code into the container.
EXPOSE 5000: Exposes port 5000 for the backend.
CMD ["node", "server.js"]: Runs the application using Node.js.
Database Dockerfile: Uses the official mongo:4.4 image directly without a custom Dockerfile.

3. Docker-Compose Networking and Port Allocation
Networks:

app-network: A custom bridge network used to facilitate communication between the frontend, backend, and db services.
Ports:

Frontend: Maps port 3000 on the host to port 3000 in the container.
Backend: Maps port 5000 on the host to port 5000 in the container.
Database: Maps port 27017 on the host to port 27017 in the container (MongoDB default port).
4. Volume Definitions and Usage
Volume: db-data
Definition: volumes: db-data:/data/db
Usage: This volume is used to persist MongoDB data across container restarts and to ensure that data is not lost when the container is recreated.
5. Git Workflow Used
Branching Strategy:

main: The primary branch containing the stable, production-ready code.
feature/<feature-name>: Branches created for developing new features or changes.
bugfix/<issue-id>: Branches for fixing specific bugs or issues.
Commit Messages:

Use clear, descriptive messages for commits to reflect the changes made (e.g., Add MongoDB connection to backend, Fix Dockerfile for frontend).
Merging:

Feature branches are merged into main using pull requests after review and testing.
6. Debugging Measures Applied if Necessary
Logs:

Used docker logs <container_id> to view logs for debugging container issues.
Interactive Shell:

Used docker exec -it <container_id> /bin/bash to access the container’s shell for troubleshooting.
Port Conflicts:

Identified and resolved port conflicts using lsof and kill commands.
7. Docker Image Tag Naming Standards
Tag Format:

<image-name>:<version> (e.g., yolo-backend:latest)
Use latest for the most recent build or specific version numbers for tagged releases.
Versioning:

Follow semantic versioning principles for clarity (e.g., v1.0.0, v1.1.0).

# Explanation of Setup

## Kubernetes Cluster

We chose GKE Autopilot for its ease of management and automatic scaling. The cluster was set up in the `europe-west1` region to optimize for geographic proximity and latency.

## Docker Images

The Docker image `my-app` was built using the Dockerfile located in the project directory. It was tagged as `mwafuga/my-app:latest` and pushed to Docker Hub to ensure it can be easily accessed by the Kubernetes cluster.

## Kubernetes Manifests

The Kubernetes manifests include:
- **Deployment**: Manages the deployment of the backend and frontend services.
- **StatefulSet**: Used for the database to ensure persistent storage.
- **Services**: Exposes the pods to the internet and facilitates internal communication.

These manifests ensure that the application is deployed correctly and can scale as needed.
