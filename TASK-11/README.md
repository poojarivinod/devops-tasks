# ToDo App – CI/CD on AWS EKS with GitHub Actions & Helm

## Project Overview

This project demonstrates an **end-to-end CI/CD pipeline** for deploying a ToDo application on **Amazon EKS (Elastic Kubernetes Service)** using:<br>

* **GitHub Actions** → CI/CD pipeline<br>
* **DockerHub** → Image repository<br>
* **Helm** → Kubernetes packaging & deployment<br>
* **EKS** → Managed Kubernetes cluster on AWS<br>
----
## Architecture Flow

1.Developer pushes code → GitHub repository.<br>
2.GitHub Actions triggers:<br>
  - Build Docker image of the app.<br>
  - Push image to DockerHub.<br>
  - Deploy app to EKS using Helm.<br>
3.EKS provisions Kubernetes resources:<br>
  - Deployment (pods)<br>
  - Service (exposed as LoadBalancer)<br>
4.Application accessible via **AWS LoadBalancer DNS**<br>

---

