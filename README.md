SIT323/SIT737 – Task 6.1C: Interacting with Kubernetes

This repository contains the source code, Dockerfile, and Kubernetes configuration files for deploying and interacting with the advanced-calculator application in a Kubernetes cluster.

Tools Used

- Git
- Visual Studio Code
- Node.js
- Docker
- Kubernetes (via Minikube or Docker Desktop)
- kubectl (Kubernetes CLI)

1.Project Structure

.
├── Dockerfile  
├── deployment.yaml  
├── service.yaml  
├── advanced-calculator.js (your Node.js app)  
└── README.md  


2. Start Kubernetes

If using Minikube:

minikube start

Or ensure Kubernetes is enabled in Docker Desktop.

3. Build Docker Image

docker build -t advanced-calculator .

4. Create Kubernetes Deployment and Service

kubectl apply -f deployment.yaml  
kubectl apply -f service.yaml

5. Check Application Status

kubectl get pods  
kubectl get services

You should see your pod with STATUS: Running and your service listed.

6. Port Forward the Service

kubectl port-forward service/advanced-calculator-service 4000:4000

Leave this terminal open while using the app.

7. Access the Application

Open your browser and go to:

http://localhost:4000

You should see the advanced-calculator application interface.

Kubernetes Configuration

deployment.yaml

apiVersion: apps/v1  
kind: Deployment  
metadata:  
  name: advanced-calculator-deployment  
spec:  
  replicas: 1  
  selector:  
    matchLabels:  
      app: advanced-calculator  
  template:  
    metadata:  
      labels:  
        app: advanced-calculator  
    spec:  
      containers:  
        - name: advanced-calculator-container  
          image: advanced-calculator:latest  
          ports:  
            - containerPort: 4000  

service.yaml

apiVersion: v1  
kind: Service  
metadata:  
  name: advanced-calculator-service  
spec:  
  selector:  
    app: advanced-calculator  
  ports:  
    - protocol: TCP  
      port: 4000  
      targetPort: 4000  
  type: ClusterIP  

Troubleshooting
- Use kubectl logs to check logs if the pod isn't running.
- Run kubectl describe pod for detailed pod events and error messages.
