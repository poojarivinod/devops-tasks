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


