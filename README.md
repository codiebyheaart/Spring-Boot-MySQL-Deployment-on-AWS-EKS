# Spring Boot + MySQL Deployment on AWS EKS
# Overview
This project demonstrates end-to-end deployment of a Spring Boot application with MySQL on AWS using containerization and Kubernetes. Jenkins is used for CI/CD and Amazon EKS is used as the Kubernetes platform.
The project reflects a real-world cloud-native setup with automated build and deployment pipeline.
Technology Stack

# Java Spring Boot
MySQL
Docker
Jenkins
GitHub
AWS EC2
AWS EKS
Kubernetes

# Architecture Flow
Developer → GitHub → Jenkins (EC2 VM) → Docker Registry → AWS EKS → Application LoadBalancer → Browser
Infrastructure
Jenkins Server

Runs on AWS EC2 (Ubuntu 22.04)
Jenkins installed manually
Docker installed
kubectl and AWS CLI installed
Pipeline executed from Jenkins UI

# Kubernetes Cluster

# AWS EKS cluster
Managed node group
Kubernetes service exposed via LoadBalancer
External access via public endpoint

Folder Structure
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── mysql-deployment.yaml
│   └── mysql-service.yaml
├── Jenkinsfile
└── README.md
Deployment Flow

Code is pushed to GitHub
Jenkins pulls latest code
Jenkins builds the application
Docker image is created
Image is pushed to registry
Jenkins deploys to Kubernetes
Kubernetes pulls new image
Application becomes publicly accessible

# Jenkins Pipeline Stages

Checkout code
Build application
Run tests
Build Docker image
Push image to registry
Deploy to AWS EKS
Verify pods

# Kubernetes Commands
Connect Jenkins VM to cluster:
bashaws eks update-kubeconfig --region us-east-1 --name demo-eks-standard
Deploy application:
bashkubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
Deploy database:
bashkubectl apply -f k8s/mysql-deployment.yaml
kubectl apply -f k8s/mysql-service.yaml
Check pods:
bashkubectl get pods
Check logs:
bashkubectl logs deployment/springboot-app
Rolling deployment:
bashkubectl rollout restart deployment springboot-app
Check external IP:
bashkubectl get svc
Key Concepts Covered

# CI/CD with Jenkins
Docker containerization
Kubernetes deployments
Pod networking
Service exposure
Rolling updates
Infrastructure management
Pod logging and debugging

# Project Outcome
This project demonstrates the following real-world skills:

CI pipeline automation
Cloud deployment workflows
Kubernetes service discovery
Container orchestration
Infrastructure reliability
DevOps troubleshooting skills

Future Enhancements

Helm charts
Secrets management
Ingress controller
Autoscaling
Monitoring and logging
Blue-Green deployments

# Author
Pankaj Verma
GitHub: https://github.com/codiebyheaart
How to Use

# Clone the repository
Configure Jenkins credentials
Connect Jenkins to EKS
Run the pipeline
Access application from LoadBalancer URL


License: MIT
