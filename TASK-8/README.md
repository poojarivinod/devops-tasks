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
create the devops-docker-task folder
```
mkdir devops-docker-task
cd devops-docker-task
```
Create index.html
```
vim index.html
```
Paste the following:
```
<h1>Hello from Docker-DevOps Task</h1>
```
---
# Part 3: Dockerfile Creation
create Dockerfile
```
vim  Dockerfile
```
Paste the following:
```
# Base Image
FROM nginx:latest

# Remove default nginx website
RUN rm -rf /usr/share/nginx/html/*

# Copy our HTML file
COPY index.html /usr/share/nginx/html/

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]

```
---
# Part 4: Build & Run Docker Image
## Build Docker Image
```
docker build -t devops-docker-task.1.0.0 .
```
## verify image
```
docker images
```
## Run container
```
docker run -d -p 8080:80 devops-docker-task:1.0.0
```
## Verify running container
```
docker ps
```
---
# Access Application
Open your browser and go to:
```
http://<public ip address of server>:8080
```
you should see
```
Hello from Docker-DevOps Task
```








