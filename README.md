# Kubernetes

### What is Kubernetes? 

Kubernetes is an open-source container orchestration system for automating software deployment, scaling, and management.

### What is a K8 Cluster?

K8s clusters allow engineers to orchestrate and monitor containers across multiple physical, virtual, and cloud servers. This decouples the containers from the underlying hardware layer and enables agile and robust deployments.

### Structure of Kubernetes

![image](https://user-images.githubusercontent.com/110126036/190130187-dcdc4032-baac-4d4a-a294-1502c9acf7a5.png)

### Inside the Agent Node 

- Pods (containers from Docker with a layer of abstraction over them)
- Services (connects alike containers e.g two apps giving them the same label)
- Secrets (allows the user to declare secrets in key-value pairs and encrypts them in base64)
- Configmap (allows the user to declare key-value pairs no encryption)

### Controller Node

- Allows for the management of all of the agent nodes (using kubectl)

## Create Nginx Deployment

```
# K8 works with API versions to declare the resources
# We have to declare the api version and the kind of service/component
# Services: deployment, service, pods, replicasets, crobjob, autoscalinggroup, horizozontalscaling

# kubectl get service_name - deployment - pods - rs
# kubectl get deploy nginx_deploy 
# kubectl get pods
# kubectl describe pod pod_name
# kubectl delete svc svc_name
# kubectl delete pod pod_name

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  
  replicas: 3

  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx-deploy
        image: sdennis3141/eng122_website:v1.1
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
        ports:
        - containerPort: 80
```
