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
# kubectl and eksctl
```
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin
kubectl version --short --client
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
```
```
eksctl create cluster --name my-cluster
```
# Helm Install
```
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```
# Configuring Email in jenkins

## Step 1: Install Required Plugin
```
1.Go to Jenkins → Manage Jenkins → Plugins
2.Install:
Email Extension Plugin
```
## Step 2: Enable App Password in Gmail
```
Since Gmail blocks less secure apps, you need to create an App Password:

1.Go to your Google Account → Security
2.Enable 2-Step Verification
3.After that, go to App passwords
4.Generate an app password (e.g., for “Mail” on “Other (Custom)”)
5.Note the 16-character password (you’ll use this in Jenkins)
```
## Step 3: Configure Email Settings in Jenkins
```
* Firstly add in jenkins credentials: username and password
* username: your@gmail.com
* password: 16character password
* description:email-cred
```
### A. Go to:
Jenkins → Manage Jenkins → System

### B. Scroll to Extended E-mail Notification section and fill:
| Field        | Value            |
|--------------|------------------|
| SMTP server  | smtp.gmail.com   |
| SMTP Port    | 465              |
| Use SSL      | ✅ Checked        |
| Use TLS      | ✅ Checked        |

In Advance add credentials of email-cred
### C. Next scroll down E-mail Notification section and fill
|Field	    |Value         |
|-----------|--------------|
|SMTP server|smtp.gmail.com|
|Use SSL	|✅ checked    |
|Use TLS	|✅ Checked    |
|SMTP Authentication|✅ Checked|

SMTP Username	your Gmail address (e.g., your@gmail.com)<br>
SMTP Password	16-digit App Password (not your Gmail password)<br>
smtp port 465<br>
reply to addresss: your@gmail.com<br>
test the mail
