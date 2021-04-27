# Developing and deploying a Node.js app from Docker to Kubernetes
# Prerequisites
In order to start off this project, we need to have following tools installed
# NodeJS Installation
https://nodejs.org/en/download/
# Install Express
$ npm install express --save

# Docker Installation
https://docs.docker.com/
Notes: Keep in mind, you must enable Kubernetes service with Docker as shown below
![image](https://user-images.githubusercontent.com/67509023/116222581-a2741d00-a746-11eb-9c48-6a28e77f82eb.png)

# Kubernetes Installation
https://kubernetes.io/docs/tasks/tools/
# Minikube installation
https://kubernetes.io/docs/tasks/tools/

# Verify Minikube
$ minikube version
minikube version: v1.11.0
commit: 57e2f55f47effe9ce396cea42a1e0eb4f611ebbd

# Run the Node app
node index.js

# Dockerizing The Node Server
docker build -t node-server .

# Create and Run the Container
$ docker run -d --name nodongo -p 3000:3000 node-server

# Upload The Image To Docker Registry Docker Hub
- First create a repo in your Docker Hub account with the name nodejs-starter
- Run the following:
Please note to replace the docker account name with your's in this case 'zeeshansdocker' with your account
# Tag
$ docker tag node-server zeeshansdocker/nodejs-starter
# Push
$ docker push zeeshansdocker/nodejs-starter:1.1

# Start The Kubernetes Cluster

$ minikube start

# Create Deployment In Kubernetes Cluster

$ kubectl create -f deploy.yaml

# Expose The Deployment To The Internet
$ kubectl expose deployment nodejs-deployment --type="LoadBalancer"

# Using MetalLB In Your Minikube Environment
$ kubectl apply -f https://raw.githubusercontent.com/google/metallb/v0.9.3/manifests/namespace.yaml
$ kubectl apply -f https://raw.githubusercontent.com/google/metallb/v0.9.3/manifests/metallb.yaml # On the first install only
$ kubectl create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)"

$ minikube ip
$ kubectl create -f configmap.yaml
$ kubectl delete svc nodejs-deployment
$ kubectl expose deployment nodejs-deployment --type="LoadBalancer"

$ kubectl get svc





