---

# Cosmocloud Deploy Helm Chart

This repository contains a Helm chart (`cosmocloud-deploy`) to deploy a full application stack consisting of:
- A **Backend** service
- A **Frontend** service
- A **Redis** database service

This chart deploys the services in a Kubernetes cluster, sets environment variables, and exposes the services using Kubernetes `Service` resources.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Chart Structure](#chart-structure)
- [Installation Steps](#installation-steps)
- [Uninstalling the Application](#uninstalling-the-application)
- [Configuration](#configuration)
- [Testing](#testing)
- [License](#license)

---

## Prerequisites

Ensure the following tools are installed on your machine:

- **Helm** (v3+): [Install Helm](https://helm.sh/docs/intro/install/)
- **kubectl**: [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- A running **Kubernetes Cluster** (e.g., Minikube, Docker Desktop, or a cloud-managed cluster)

---

## Chart Structure

The Helm chart `cosmocloud-deploy` has the following structure:

```
cosmocloud-deploy/
├── Chart.yaml             # Metadata for the Helm chart
├── values.yaml            # Default configuration values
└── templates/
    ├── backend-deployment.yaml    # Backend Deployment
    ├── frontend-deployment.yaml   # Frontend Deployment
    ├── redis-deployment.yaml      # Redis Deployment
    ├── backend-service.yaml       # Backend Service (ClusterIP)
    ├── frontend-service.yaml      # Frontend Service (NodePort)
    └── redis-service.yaml         # Redis Service (ClusterIP)
```

---

## Installation Steps

### 1. Clone this repository:

```bash
git clone <repository-url>
cd cosmocloud-deploy
```

### 2. Install the Helm Chart:

To install the chart in your Kubernetes cluster, run:

```bash
helm install testapp ./cosmocloud-deploy --atomic --timeout 30s
```

This will deploy the following services:
- **Backend** (`shreybatra/sample-backend`)
- **Frontend** (`shreybatra/sample-frontend`)
- **Redis** (`redis`)

### 3. Verify the Deployment:

Check that the Pods and Services are running successfully:

```bash
kubectl get pods
kubectl get services
```

---

## Uninstalling the Application

To uninstall the application and remove the resources, run:

```bash
helm uninstall testapp
```

This will delete all resources (pods, services, deployments) related to the `testapp` release.

---

## Configuration

You can customize the following configurations in the `values.yaml` file:

- **Backend Image**:
  Set the backend Docker image:
  ```yaml
  backend:
    image: shreybatra/sample-backend
  ```

- **Frontend Image**:
  Set the frontend Docker image:
  ```yaml
  frontend:
    image: shreybatra/sample-frontend
  ```

- **Redis Image**:
  Set the Redis Docker image:
  ```yaml
  redis:
    image: redis
  ```

- **Environment Variables**:
  Set environment variables for each service:
  ```yaml
  backend:
    env:
      REDIS_URI: redis://redis-svc:6379

  frontend:
    env:
      BACKEND_URL: http://backend-svc:8000
  ```

---

## Testing

After deployment, you can access the services as follows:

- **Backend Service** (ClusterIP): Access within the cluster at `backend-svc:8000`
- **Frontend Service** (NodePort): Expose the frontend externally at `http://<node-ip>:31000`
- **Redis Service** (ClusterIP): Access within the cluster at `redis-svc:6379`

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

This `README.md` file provides a structured overview of the chart, installation steps, and how to configure it. You can copy it directly into your project’s root directory to ensure that users can easily understand how to deploy and manage the application stack.