# static-html-docker-server-kubernetes-deployment
Steps for Deploying a Static HTML Site with Docker   

* docker build -t index-app:v1 .

* docker run -d -p 80:80 index-app:v1

* docker ps

* docker container 

* docker image list

Steps for push to dockerhub repository

* docker tag index-app:v1 bungyan07/index-app:v1

* docker login 

* docker push bungyan07/index-app:v1

# Architecture

# Service Deployment Into Kubernetes
Kubernetes service yaml = default

* apiVersion: apps/v1
kind: Deployment
metadata:
  name: index-app-deployment
  labels:
    app: index-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: index-app
  template:
    metadata:
      labels:
        app: index-app
    spec:
      containers:
      - name: index-app
        image: bungyan07/index-app:v1
        ports:
        - containerPort: 80
        resources:
          limits:
            cpu: 500m
            memory: 200Mi
          requests:
            cpu: 200m
            memory: 100Mi
---
apiVersion: v1
kind: Service
metadata:
  name: index-app-service
  
spec:
  selector:
    app: index-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer

  # Service Deployment Into Kubernetes from namespaces
Kubernetes service yaml = dev

apiVersion: apps/v1
kind: Deployment
metadata:
  name: index-app-deployment
  namespace: dev
  labels:
    app: index-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: index-app
  template:
    metadata:
      labels:
        app: index-app
    spec:
      containers:
      - name: index-app
        image: bungyan07/index-app:v1
        ports:
        - containerPort: 80
        resources:
          limits:
            cpu: 500m
            memory: 200Mi
          requests:
            cpu: 200m
            memory: 100Mi
---
apiVersion: v1
kind: Service
metadata:
  name: index-app-service
  namespace: dev

spec:
  selector:
    app: index-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer

  # Service Deployment Into Kubernetes from namespaces
Kubernetes service yaml = staging
apiVersion: apps/v1
kind: Deployment
metadata:
  name: index-app-deployment
  namespace: staging
  labels:
    app: index-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: index-app
  template:
    metadata:
      labels:
        app: index-app
    spec:
      containers:
      - name: index-app
        image: bungyan07/index-app:v1
        ports:
        - containerPort: 80
        resources:
          limits:
            cpu: 500m
            memory: 200Mi
          requests:
            cpu: 200m
            memory: 100Mi
---
apiVersion: v1
kind: Service
metadata:
  name: index-app-service
  namespace: staging

spec:
  selector:
    app: index-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer

 # Service Deployment Into Kubernetes from namespaces
Kubernetes service yaml = prod

apiVersion: apps/v1
kind: Deployment
metadata:
  name: index-app-deployment
  namespace: prod
  labels:
    app: index-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: index-app
  template:
    metadata:
      labels:
        app: index-app
    spec:
      containers:
      - name: index-app
        image: bungyan07/index-app:v1
        ports:
        - containerPort: 80
        resources:
          limits:
            cpu: 500m
            memory: 200Mi
          requests:
            cpu: 200m
            memory: 100Mi
---
apiVersion: v1
kind: Service
metadata:
  name: index-app-service
  namespace: prod

spec:
  selector:
    app: index-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer

  # Run Service Deployment Into Kubernetes 
kubectl apply -f yaml -n (namespaces)

  # add horizontal pod autoscaling on web app with cpu and memory metrics
Kubernetes service yaml = hpa-cpu

apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: index-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: index-app-deployment
  minReplicas: 3
  maxReplicas: 10
  targetCPUUtilizationPercentage: 50

Kubernetes service yaml = hpa-mem

apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: index-app-hpa-memory
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: index-app-deployment
  minReplicas: 3
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageValue: 50Mi

  # Run Service HPA Deployment Into Kubernetes 
kubectl apply -f yaml -n 
 












