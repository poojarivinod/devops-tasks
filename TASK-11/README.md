# ToDo App – CI/CD on AWS EKS with GitHub Actions & Helm

## Project Overview

This project demonstrates an **end-to-end CI/CD pipeline** for deploying a ToDo application on **Amazon EKS (Elastic Kubernetes Service)** using:<br>

* **GitHub Actions** → CI/CD pipeline<br>
* **DockerHub** → Image repository<br>
* **Helm** → Kubernetes packaging & deployment
* **EKS** → Managed Kubernetes cluster on AWS<br>
----
## Architecture Flow

1. Developer pushes code → GitHub repository.
2. GitHub Actions triggers:
   - Build Docker image of the app.
   - Push image to DockerHub.
   - Deploy app to EKS using Helm.
3. EKS provisions Kubernetes resources:
   - Deployment (pods)
   - Service (exposed as LoadBalancer)
4. Application accessible via **AWS LoadBalancer DNS**

---

