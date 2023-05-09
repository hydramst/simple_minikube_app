# simple_minikube_app
This is demonstration example of web application, running on Minikube cluster locally. 

<img width="308" alt="image" src="https://github.com/hydramst/simple_minikube_app/assets/44744458/c345719d-03a9-44c0-90d5-e74135fafa2b">

### Prerequisites

- Docker and Docker Compose
- Minikube
- kubectl

### Project Structure

```
kubernetes/
├── redis/
│   ├── deployment.yaml
│   └── service.yaml
└── streamlit/
    ├── deployment.yaml
    └── service.yaml
```

### Steps

1. Start Minikube: 

   ```bash
   minikube start
   ```
   
2. Set the Docker environment variables: 

   ```bash
   eval $(minikube docker-env)
   ```
   
3. Build the Docker images for Streamlit and Redis: 

   ```bash
   docker build -t hydramst/aniemore_streamlit:latest streamlit/.
   docker build -t redis:latest redis/.
   ```
   
4. Deploy Redis: 

   ```bash
   kubectl apply -f kubernetes/redis/redis-deployment.yaml
   kubectl apply -f kubernetes/redis/redis-service.yaml
   ```
   
5. Verify Redis deployment: 

   ```bash
   kubectl get pods
   kubectl get services
   ```
   
6. Deploy Streamlit: 

   ```bash
   kubectl apply -f kubernetes/streamlit/streamlit-deployment.yaml
   kubectl apply -f kubernetes/streamlit/streamlit-service.yaml
   ```
   
7. Verify Streamlit deployment: 

   ```bash
   minikube service streamlit-service
   ```
   
   This should open a browser window with the Streamlit application running.
   
8. To clean up, delete the Kubernetes resources: 

   ```bash
   kubectl delete deployment streamlit-deployment
   kubectl delete service streamlit-service
   kubectl delete deployment redis-deployment
   kubectl delete service redis-service
   ```
   
   Stop Minikube: 

   ```bash
   minikube stop
   ```
