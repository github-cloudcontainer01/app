#  CI/CD Pipeline using Jenkins, Docker & Kubernetes

##  Project Overview

This project demonstrates a complete **CI/CD (Continuous Integration and Continuous Deployment)** pipeline for a containerized Node.js application.

Whenever code is pushed to the GitHub repository, Jenkins automatically triggers the pipeline to:

* Checkout the latest source code
* Build a Docker image
* Run application tests
* Push the Docker image to Docker Hub
* Deploy the latest application to a Kubernetes cluster

The application is deployed on a **single-node Kubernetes cluster (kubeadm)** running on an **AWS EC2 t3.medium** instance.

---

#  Tools & Technologies Used

| Tool                   | Purpose                    |
| ---------------------- | -------------------------- |
| Git                    | Version Control            |
| GitHub                 | Source Code Repository     |
| Jenkins                | CI/CD Automation           |
| Docker                 | Containerization           |
| Docker Hub             | Container Image Registry   |
| Kubernetes (kubeadm)   | Container Orchestration    |
| kubectl                | Kubernetes CLI             |
| Prometheus             | Monitoring                 |
| Grafana                | Visualization & Dashboards |
| AWS EC2 (Ubuntu 22.04) | Hosting Infrastructure     |
| Node.js                | Sample Application         |

---

#  Project Architecture

```text
Developer
    │
    │ Git Push
    ▼
GitHub Repository
    │
    │ Webhook
    ▼
Jenkins Pipeline
    │
    ├── Checkout Source Code
    ├── Build Docker Image
    ├── Run Tests
    ├── Push Image to Docker Hub
    └── Deploy to Kubernetes
                    │
                    ▼
            Kubernetes Cluster
                    │
                    ▼
             Application Pod
                    │
                    ▼
             NodePort Service
                    │
                    ▼
             Application URL
```

---

#  Project Structure

```text
sample-app/
│
├── app.js
├── package.json
├── Dockerfile
├── Jenkinsfile
├── .env.example
├── README.md
├── deployment.yaml
└── service.yaml
```

---

# Step 1 – Source Code Management

The application source code is stored in a GitHub repository.

The repository contains:

* Application source code
* Dockerfile
* Jenkinsfile
* Kubernetes deployment files
* Environment variable example file
* README documentation

Clone the repository:

```bash
git clone https://github.com/github-cloudcontainer01/app.git
cd app
```

---

# Step 2 – Dockerize the Application

A Dockerfile is used to package the Node.js application into a Docker image.

Build the Docker image:

```bash
docker build -t sample-app .
```

Run the container:

```bash
docker run -d -p 3000:3000 sample-app
```

Verify the application:

```
http://localhost:3000
```

---

# Step 3 – Configure Jenkins CI/CD Pipeline

A Jenkins Pipeline is configured using the **Jenkinsfile** stored in the repository.

The pipeline performs the following stages:

* Checkout
* Build
* Test
* Push Docker Image
* Deploy to Kubernetes

Whenever code is pushed to GitHub, a **GitHub Webhook** automatically triggers the Jenkins pipeline.

---

# Step 4 – Push Docker Image to Docker Hub

After a successful build and test, Jenkins pushes the Docker image to Docker Hub.

Commands used:

```bash
docker login

docker tag sample-app dpravin7/sample-app:latest

docker push dpravin7/sample-app:latest
```

---

# Step 5 – Deploy to Kubernetes

The application is deployed to a **single-node Kubernetes cluster** created using **kubeadm**.

Deployment:

```bash
kubectl apply -f deployment.yaml
```

Service:

```bash
kubectl apply -f service.yaml
```

Check deployment:

```bash
kubectl get pods

kubectl get svc
```

Access the application:

```
http://15.206.97.98:30669
```

---

# Step 6 – Monitoring

Monitoring is configured using:

* Prometheus
* Grafana

The following metrics are monitored:

* CPU Usage
* Memory Usage
* Pod Health
* Container Status

---

# Jenkins Pipeline Workflow

```text
Git Push
    │
    ▼
GitHub Webhook
    │
    ▼
Jenkins Pipeline
    │
    ├── Checkout
    ├── Build Docker Image
    ├── Run Tests
    ├── Push Image
    └── Deploy to Kubernetes
```

---

# Deliverables

* GitHub Repository
* Dockerfile
* Jenkinsfile
* Kubernetes Deployment YAML
* Kubernetes Service YAML
* Docker Hub Image
* Running Application URL
* Prometheus & Grafana Monitoring

---

# Expected CI/CD Flow

```text
Developer
      │
      ▼
Git Push
      │
      ▼
GitHub Repository
      │
      ▼
GitHub Webhook
      │
      ▼
Jenkins Pipeline
      │
      ▼
Build Docker Image
      │
      ▼
Push Image to Docker Hub
      │
      ▼
Deploy to Kubernetes
      │
      ▼
Application Available
```

---

# Conclusion

This project demonstrates a complete CI/CD workflow using Jenkins, Docker, Kubernetes, and GitHub. The pipeline automatically builds, tests, and deploys the application whenever new code is pushed to the repository, providing a simple and efficient deployment process.

Deliverables
1. GitHub repository link  : https://github.com/github-cloudcontainer01/app.git
2. Running application URL : 15.206.97.98:30669
3. Monitoring URL          : 15.206.97.98:31237
