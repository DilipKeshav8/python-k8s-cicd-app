# Python Kubernetes CI/CD Pipeline 🚀🐳☸️

A simple Python Flask web application deployed on Kubernetes with a fully automated CI/CD pipeline powered by Jenkins and Docker.

---

## Project Overview

This project demonstrates how to build, containerize, and deploy a Python Flask app on a Kubernetes cluster. It integrates Jenkins to automate the entire pipeline — from building the Docker image, pushing it to Docker Hub, to deploying the latest version on Kubernetes. This setup offers a hands-on example of continuous integration and continuous delivery (CI/CD) for cloud-native applications.

---

## Features

- **Python Flask Web Application**: Lightweight REST API backend.
- **Docker Containerization**: Containerizes the Flask app for portability.
- **Kubernetes Deployment**: Uses manifests for deployment and service.
- **Automated CI/CD Pipeline**: Jenkins pipeline automates build, push, and deployment.
- **Docker Hub Integration**: Stores and manages Docker images centrally.

---

## Technologies Used

| Technology       | Description                             |
|------------------|-------------------------------------|
| Python & Flask 🐍  | Backend web framework                |
| Docker 🐳          | Containerization technology          |
| Kubernetes ☸️      | Container orchestration platform      |
| Jenkins 🔧        | Automation server for CI/CD           |
| Git & GitHub 🌐    | Version control and source repository |
| Docker Hub 📦     | Docker image registry                  |

---

## Prerequisites

Before you begin, ensure you have met the following requirements:

- Docker installed and running  
- Kubernetes cluster (Minikube or cloud-based) configured  
- Jenkins installed and accessible  
- Docker Hub account with credentials ready  
- Git installed



Project Structure

python-kubernetes-cicd/
│
├── app/                    # Flask application source code
├── k8s/                    # Kubernetes deployment and service manifests
│   ├── deployment.yaml
│   └── service.yaml
├── Jenkinsfile             # Jenkins pipeline configuration
├── Dockerfile              # Docker image specification
└── README.md               # Project documentation

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/python-kubernetes-cicd.git
cd python-kubernetes-cicd

2. Build Docker Image Locally (Optional)

docker build -t yourdockerhubusername/flask-app:latest .


3. Push Docker Image to Docker Hub

docker push yourdockerhubusername/flask-app:latest

4. Deploy to Kubernetes

Apply Kubernetes manifests:

kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml


5. Jenkins Pipeline

Configure Jenkins credentials for Docker Hub and Kubernetes access.

Import Jenkinsfile from the repository.

Run the Jenkins pipeline to automate building, pushing, and deploying.

Accessing the Application

After deployment, the Flask app will be accessible via the Kubernetes service. If using Minikube:

minikube service flask-service
Or use the NodePort/LoadBalancer IP depending on your cluster setup.


Author
Dilip Keshav

Feel free to reach out for questions, feedback, or collaboration opportunities!

License
This project is licensed under the MIT License - see the LICENSE file for details.

Acknowledgements
Thanks to the open-source community for the tools and inspiration that made this project possible!

Happy Deploying! 🎉


