# todo_cicd_end-end_project

### How to test locally or Manually ?
Create Amazon linux EC2 Instance to test it locally .
```
yum install git -y
cd /opt
git clone https://github.com/jadalaramani/todo_cicd_end-end_project.git
cd todo_cicd_end-end_project/
cd backend/
```
```
curl -fsSL https://rpm.nodesource.com/setup_22.x | bash -
yum install -y nodejs
npm install
npm start  ( optional ) 
node server.js & 
```
---> now access from browser with port 3000 ( PublicIP:3000 )
```
ps aux | grep node
kill PID
```
stops running application
### install the docker
```
yum install docker -y
systemctl start docker
systemctl enable docker
systemctl status docker
```
```
docker build -t todo:1.0.0 -f Dockerfile .
```
build the docker image
```
docker run -d -p 8080:3000 todo:1.0.0
```
run the docker image<br>
---> now access from browser with port 3000 ( PublicIP:3000 )
```
curl http://localhost:3000
```
# Todo project using the jenkins
Create Amazon linux EC2 Instance execute following commands
```
yum install git -y
cd /opt
git clone https://github.com/jadalaramani/todo_cicd_end-end_project.git
```
### Jenkins Installation on Amazon Linux
```
sudo yum update -y
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum upgrade
sudo yum install java-17-amazon-corretto -y
sudo yum install jenkins -y
sudo systemctl enable jenkins
systemctl start jenkins
```
Browse in google with <pulic ip of server>:8080

### Docker Installation
```
yum install docker -y
systemctl start docker
systemctl enable docker
sudo usermod -aG docker jenkins
sudo chmod 666 /var/run/docker.sock
sudo systemctl restart docker
```
jenkins user is added to the docker group, gives the read and write permission to the docker group

### SonarQube Setup
Ensure SonarQube is up and running (local or cloud).
```
docker run -itd --name sonar -p 9000:9000 sonarqube
```
```
docker ps
```
we can see the sonarqube container is running
In browser search as <public ip server>:9000

In Jenkins:
* Install the SonarQube Scanner for Jenkins plugin.
* Add credentials (usually a Sonar token).
* Add your SonarQube server in Manage Jenkins > Configure System > SonarQube servers.(It will give the jenkins to access the sonarqube) 
* also update in Global tool settings of SonarQubeScanner ( Manage Jenkins > tools > add installation)

### Configure Quality Gate in SonarQube

* Create or Edit a Quality Gate in SonarQube

* Log in to SonarQube as an admin → Quality Gates tab.

* Either edit “Sonar way” or click “Create” to build your own gate.

* Click “Set as Default” so every new project—and therefore your todo-node-app—uses it automatically.

* Add a Webhook for Jenkins in sonarqube
* SonarQube pushes Quality Gate results back to Jenkins through a webhook call.

* SonarQube → Administration ▶ Configuration ▶ Webhooks.

* Click “Create”

Name: sonarqube-webhook

URL: http://<JENKINS_URL>/sonarqube-webhook/

Save.

### Jenkins with Below plugins 
```
Kubernetes CLI plugin

Kubernetes

Kubernetes client api

Kubernetes credentials

k8s credential provider

Docker

Docker Pipeline plugin

Email Extention template

Pipeline stage view

Sonarqube Scanner

Blue ocean
```
