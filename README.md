# Kubernetes
A good guide to start kubernetes...........

# Containers and Containerization
I hope you are familiar with Virtual Machines and virtualization

The overall goal is to use resources efficiently.

Containers are lightweight, portable, and self-contained environments that allow software to run consistently across different computing environments. They package an application and all of its dependencies, libraries, and configuration files into a single unit, making it easier to develop, test, and deploy software.
A container is essentially a virtualized environment, but unlike virtual machines (VMs), containers do not require a full operating system (OS) to run. Instead, they share the OS kernel of the host machine, which makes them more lightweight and faster to start compared to VMs.

Containerization is the process of encapsulating an application and its dependencies in a container. It involves using container technologies (such as Docker) to package applications, ensuring that the application behaves consistently regardless of where it is deployed.

In containerization, the environment in which the application runs is isolated from the host system and other containers. This allows for a consistent execution environment across different systems.


# Kubernetes, also known as K8s, is an open source system for automating deployment, scaling, and management of containerized applications.

you can say a kind of orchestration tool.
output after setting up
![image](https://github.com/user-attachments/assets/71c9b764-5687-4817-a2c8-d360adb4fb37)



Key Components and Their Purpose
Secret (secret.yaml):

Stores Base64-encoded MongoDB admin username and password.
Ensures sensitive credentials are not hard-coded in the configuration files.
Config Map (mongo-config.yaml):

Stores the MongoDB service URL (mongo-service).
Allows reusability and decouples the MongoDB connection information.
MongoDB Deployment (mongo-app.yaml):

Deploys a MongoDB instance with one replica.
Uses the secret for its initialization (MONGO_INITDB_ROOT_USERNAME and MONGO_INITDB_ROOT_PASSWORD).
MongoDB Service (mongo-app.yaml):

Exposes MongoDB to other pods in the cluster using a ClusterIP service.
Allows Mongo Express to connect to MongoDB via the service name (mongo-service).
Mongo Express Deployment (web-app.yaml):

Deploys the Mongo Express web interface for managing MongoDB.
Retrieves MongoDB connection details and admin credentials via environment variables (ME_CONFIG_MONGODB_SERVER, ME_CONFIG_MONGODB_ADMINUSERNAME, ME_CONFIG_MONGODB_ADMINPASSWORD).
Mongo Express Service (web-app.yaml):

Exposes Mongo Express as a NodePort service, making it accessible externally through the Minikube IP.
Important Steps Taken
Environment Variables:

Environment variables in web-app.yaml allow Mongo Express to connect to MongoDB using:
MongoDB server name from the ConfigMap.
Admin username and password from the Secret.
Service Discovery:

Kubernetes' DNS resolves the mongo-service name to the MongoDB pod's ClusterIP.
Separation of Concerns:

Secrets and ConfigMaps decouple sensitive data (credentials) and configuration (MongoDB URL) from the application code, improving security and maintainability.
Exposing Mongo Express:

The NodePort service exposes Mongo Express on http://<minikube-ip>:30100, allowing you to manage MongoDB via a web interface.
