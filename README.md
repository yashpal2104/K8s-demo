# Kubernetes Demo Project

This project demonstrates the deployment of a demo application using Kubernetes and Minikube. The application consists of a MongoDB database and a web application that connects to the database. The purpose of this project is to help understand key Kubernetes concepts such as Deployments, Services, ConfigMaps, and Secrets.

## Prerequisites

- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Docker](https://www.docker.com/get-started)

## Project Structure

- `mongo-config.yaml`: ConfigMap for MongoDB configuration.
- `mongo-secrets.yaml`: Secret for MongoDB credentials.
- `mongo.yaml`: Deployment and Service for MongoDB.
- `webapp.yaml`: Deployment and Service for the web application.

## Setup

### Step 1: Start Minikube

```sh
minikube start
```
### Step 2: Apply Configurations
1. Apply MongoDB ConfigMap

```sh
kubectl apply -f mongo-config.yaml
```
2. Apply MongoDB Secrets
```sh
kubectl apply -f mongo-secrets.yaml
```
3. Deploy MongoDB
```sh
kubectl apply -f mongo.yaml
```
4. Deploy Web Application
```sh
kubectl apply -f webapp.yaml
```

### Step 3: Customizing the Application
Using a Different Web Application Image. You can use any webapp to deploy as long it exists in the [Docker Hub](https://hub.docker.com/).
The `webapp.yaml` file specifies the Docker image for the web application:

```YAML
containers:
- name: webapp
  image: nanajanashia/k8s-demo-app:v1.0
```
You can change the image field to use your own Docker image. For more information on Docker images, visit the [Docker Hub](https://hub.docker.com/).

Using a Different MongoDB Image
The mongo.yaml file specifies the Docker image for MongoDB:

```YAML
containers:
- name: mongodb
  image: mongo:5.0
```
You can change the image field to use a different version of MongoDB or your own custom image. Refer to the [MongoDB images on Docker Hub](https://hub.docker.com/_/mongo) for more options.
### Step 4: Access the Application
5. To access the web application, you need to get the Minikube IP and the NodePort.

```sh
minikube ip
```
```sh
kubectl get svc webapp-service
```
### Step 5: Use the Minikube IP and the NodePort to access the application in your browser. For example:
```sh
yoshi@yodaone ~/VSCode/K8s-demo$ minikube ip
192.168.49.2

yoshi@yodaone ~/VSCode/K8s-demo$ kubectl get svc -o wide
NAME             TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE    SELECTOR
kubernetes       ClusterIP   10.96.0.1       <none>        443/TCP          152m   <none>
mongo-service    ClusterIP   10.105.172.29   <none>        27017/TCP        22m    app=mongo
webapp-service   NodePort    10.101.3.177    <none>        3000:30100/TCP   21m    app=webapp
```
In this case, the Minikube IP is 192.168.49.2 and the NodePort is 30100. You can access the application in your browser using:
``` sh
http://192.168.49.2:30100
```
### Clean Up
6. To delete the resources created for this demo, run the following commands:

```sh
kubectl delete -f webapp.yaml
kubectl delete -f mongo.yaml
kubectl delete -f mongo-secrets.yaml
kubectl delete -f mongo-config.yaml
minikube stop
```
### Conclusion
This project provides a basic understanding of deploying applications on Kubernetes using Minikube. It covers essential concepts such as Deployments, Services, ConfigMaps, and Secrets. For more advanced Kubernetes features, refer to the [official documentation](https://kubernetes.io/docs/home/).
