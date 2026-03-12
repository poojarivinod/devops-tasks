# CI/CD Pipeline Documentation: EC2 + Jenkins + Ansible + Docker
## Infrastructure Overview
* Cloud Provider: AWS
* Instance Type: t3.micro
* AMI: ubuntu

## Software Installation
### 1. Update System
```
sudo yum update -y
```
### 2. Install Docker
```
sudo yum install -y docker
sudo systemctl start docker
sudo systemctl enable docker
```
### 3. Install Ansible
```
sudo yum install ansible -y
```
### 4. Install Jenkins
```
sudo yum update -y
sudo wget -O /etc/yum.repos.d/jenkins.repo  https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum upgrade
sudo yum install java-21-amazon-corretto -y
sudo yum install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
```
```
sudo usermod -aG docker jenkins
```
## Jenkins Job Configuration
### Job Name: Build-and-Deploy-App

Stage 1: Clone Git Repository
Repository URL: https://github.com/adarsh0331/Project_06_Ansible_Docker
Branch: main
Credentials: SSH key or GitHub token (if private)
Stage 2: Trigger Ansible Playbook
Build Step: Execute shell
```
ansible-playbook playbook.yml
```
## Validation Steps
1.Check Jenkins Console Output for success.
2.Verify Docker Container:
```
docker ps
curl http://localhost:80
```
3.Access Web App via EC2 public IP: http://<your-ec2-ip>:80
