# Task2_Kaiburr
**# Task Manager API - Kubernetes Deployment  This task extends the Task Manager API by containerizing the application using Docker and deploying it to a Kubernetes cluster. It also modifies the "PUT a TaskExecution" endpoint to create a new Kubernetes pod for running shell commands.
# Task Manager API - Kubernetes Deployment**

This task extends the Task Manager API by containerizing the application using Docker and deploying it to a Kubernetes cluster. It also modifies the "PUT a TaskExecution" endpoint to create a new Kubernetes pod for running shell commands.

## Features
- **Dockerized Application**: Create Docker images for the API and deploy it in Kubernetes.
- **Kubernetes Deployment**: Deploy the API and MongoDB as separate pods.
- **Persistent Storage**: Use a persistent volume for MongoDB to ensure data persistence.
- **Environment Variables**: MongoDB connection details are passed as environment variables.
- **Task Execution in Kubernetes Pods**: Instead of running shell commands locally, a new Kubernetes pod is created for execution.

## Prerequisites
- Docker
- Kubernetes (Minikube, Docker Desktop, Kind, or a cloud provider like EKS/AKS/GKE)
- kubectl
- Helm (for MongoDB deployment)

## Steps to Deploy
### 1. Clone Repository
```sh
git clone https://github.com/your-username/task-manager-api.git
cd task-manager-api
```

### 2. Build Docker Images
```sh
docker build -t task-manager-api .
```

### 3. Deploy MongoDB with Helm
```sh
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install mongodb bitnami/mongodb --set persistence.enabled=true
```

### 4. Apply Kubernetes Manifests
```sh
kubectl apply -f k8s/mongo-pvc.yaml
kubectl apply -f k8s/mongo-deployment.yaml
kubectl apply -f k8s/task-api-deployment.yaml
kubectl apply -f k8s/task-api-service.yaml
```

### 5. Verify Deployment
```sh
kubectl get pods
kubectl get services
```

### 6. Test API Endpoints
Use `curl` or Postman to test the deployed API.
```sh
curl -X GET "http://<node-ip>:<node-port>/tasks"
```

### 7. Modify Task Execution to Run in Kubernetes Pod
- The `PUT /tasks/{id}/execute` endpoint now creates a new Kubernetes pod using the BusyBox image and runs the provided command inside it.

## Screenshots
(Include `kubectl` command outputs, pod list, service details, and API response screenshots)

## License
MIT License

