# Overview
The deployment consists of two major components:

- MongoDB Database<b>
- Mongo-Express (a web-based admin interface for MongoDB)<b>
  
Each component is deployed using Kubernetes resources such as ConfigMaps, Secrets, Deployments and Services.

## Prerequisites
- Docker<b>
- Minikube<b>
- Kubectl or another Kubernetes management tool<b>
- Deployment Files<b>
  
The repository contains the following Kubernetes configuration files to deploy a MongoDB database and its web-based admin interface, Mongo-Express.

### mongo-configmap.yaml

This file holds the configuration map used in the MongoDB and Mongo-Express deployments. It contains the database URL which is utilized by Mongo-Express to connect to the MongoDB database.

### mongo-express.yaml

This is a two-part YAML file which includes:

The Deployment configuration for Mongo-Express. It references the MongoDB connection information stored in the ConfigMap and Secret to access the MongoDB database. The image used is the official mongo-express Docker image.

The Service configuration to expose the Mongo-Express deployment to the network. It utilizes the LoadBalancer service type to make the service accessible outside of the Kubernetes cluster.

### mongo-secret.yaml

This file holds the Secrets used for the MongoDB deployment. It contains the base64 encoded MongoDB admin username and password, which are used by both the MongoDB and Mongo-Express deployments.

### mongodb.yaml

This is also a two-part YAML file which includes:

The Deployment configuration for MongoDB. It utilizes the official mongo Docker image, and references the admin username and password stored in the Secret.

The Service configuration which exposes the MongoDB deployment to the network, enabling Mongo-Express and potentially other applications to connect to the database.

## Deployment Instructions

1. Clone this repository.<b>
2. Start the Minikube cluster with the command:
   
```bash
minikube start
```

3. The commands for deployment are as follows:

```bash
kubectl apply -f mongo-configmap.yaml
kubectl apply -f mongo-secret.yaml
kubectl apply -f mongodb.yaml
kubectl apply -f mongo-express.yaml
```

## Accessing the Applications

MongoDB is running on port 27017 and Mongo-Express on port 8081. As the services are set up with type LoadBalancer and we are using Minikube, you can access the Mongo-Express web interface via a web browser by running the command:

```bash
minikube service mongo-express-service
```

This command will automatically open the service in your default web browser.
