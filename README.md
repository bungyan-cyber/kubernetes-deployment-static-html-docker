# Static HTML Docker Server Kubernetes Deployment

This repository provides a guide and configurations for deploying a static HTML site using Docker and Kubernetes. The steps outlined below cover the Docker build process, pushing the image to Docker Hub, and deploying the service into Kubernetes with namespaces.

**Table of Contents**
- [Docker Build and Run](#docker-build-and-run)
- [Push to Docker Hub](#push-to-docker-hub)
- [Kubernetes Deployment](#kubernetes-deployment)
  - [Create Kubernetes Namespace](#create-kubernetes-namespace)
  - [Service Deployment from Namespaces](#service-deployment-from-namespaces)
  - [Run Kubernetes Service Deployment](#run-kubernetes-service-deployment)
  - [Horizontal Pod Autoscaling](#horizontal-pod-autoscaling)

## Docker Build and Run <a name="docker-build-and-run"></a>

Build and run the Docker container locally using the following commands:

```bash
docker build -t index-app:v1 .
docker run -d -p 80:80 index-app:v1
docker ps
docker container list
docker image list
```

## Push to Docker Hub <a name="push-to-docker-hub"></a>

Push the Docker image to the Docker Hub repository:

```bash
docker tag index-app:v1 bungyan07/index-app:v1
docker login 
docker push bungyan07/index-app:v1
```

## Kubernetes Deployment <a name="kubernetes-deployment"></a>

### Create Kubernetes Namespace <a name="create-kubernetes-namespace"></a>

Create Kubernetes namespaces for staging, production, and development:

```bash
kubectl create namespace staging
kubectl create namespace production
kubectl create namespace dev
```

### Service Deployment from Namespaces <a name="service-deployment-from-namespaces"></a>

For each namespace, deploy the service using the respective YAML file:

- **Development Namespace:**
  ```bash
  kubectl apply -f dev-service.yaml -n dev
  ```

- **Staging Namespace:**
  ```bash
  kubectl apply -f staging-service.yaml -n staging
  ```

- **Production Namespace:**
  ```bash
  kubectl apply -f prod-service.yaml -n production
  ```

### Run Kubernetes Service Deployment <a name="run-kubernetes-service-deployment"></a>

Apply the Kubernetes YAML files to deploy the service:

```bash
kubectl apply -f dev-service.yaml -n dev
kubectl apply -f staging-service.yaml -n staging
kubectl apply -f prod-service.yaml -n production
```

### Horizontal Pod Autoscaling <a name="horizontal-pod-autoscaling"></a>

Add horizontal pod autoscaling to the web app with CPU and memory metrics:

```bash
kubectl apply -f hpa.yaml
kubectl get pods 
kubectl get pods --all-namespaces -o wide
kubectl get pod -o wide
kubectl get services
kubectl get pods --all-namespaces
kubectl get hpa
```

Apply the Horizontal Pod Autoscaling configuration:

```bash
kubectl apply -f hpa.yaml -n <namespace>
```

These steps cover building a Docker image, pushing it to Docker Hub, and deploying the static HTML site into Kubernetes with namespaces and horizontal pod autoscaling. Adjust configurations as needed for your specific environment and requirements.

Feel free to reach out if you have any questions or need further assistance!
