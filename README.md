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
Apply MongoDB ConfigMap

```sh
kubectl apply -f mongo-config.yaml
```
Apply MongoDB Secrets
```sh
kubectl apply -f mongo-secrets.yaml
```
Deploy MongoDB
```sh
kubectl apply -f mongo.yaml
```
Deploy Web Application
```sh
kubectl apply -f webapp.yaml
```
### Step 3: Access the Application
To access the web application, you need to get the Minikube IP and the NodePort.

```sh
minikube ip
```
```sh
kubectl get svc webapp-service
```
Use the Minikube IP and the NodePort to access the application in your browser.

### Clean Up
To delete the resources created for this demo, run the following commands:

```sh
kubectl delete -f webapp.yaml
kubectl delete -f mongo.yaml
kubectl delete -f mongo-secrets.yaml
kubectl delete -f mongo-config.yaml
minikube stop
```
### Conclusion
This project provides a basic understanding of deploying applications on Kubernetes using Minikube. It covers essential concepts such as Deployments, Services, ConfigMaps, and Secrets. For more advanced Kubernetes features, refer to the official documentation.
