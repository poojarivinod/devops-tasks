# DevOps Docker Task – Static HTML Website using Nginx

## Objective

Learn how to containerize a simple application using Docker, manage Docker images and containers, and understand basic DevOps workflow.

---
# Part 1: Environment Setup
## Install Docker
```
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
### start and enable the Docker
```
sudo systemctl start docker
sudo systemctl enable docker
```

### verify the Docker
```
sudo systemctl status docker
docker --version
```
---
# Part 2: Create a Simple Application
```
mkdir devops-docker-task
cd devops-docker-task
```
```
vim index.html
```
```
<h1>Hello from Docker-DevOps Task</h1>
```
---
# Part 3: Dockerfile Creation
```
vim  Dockerfile
```
```
# Base Image
FROM nginx:latest

# Set Working Directory
WORKDIR /usr/share/nginx/html

# Remove default files
RUN rm -rf ./*

# Copy application files
COPY index.html .

# Expose required port
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
```





