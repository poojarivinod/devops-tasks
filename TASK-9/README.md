# Task:9

## objective

Terraform State Migration to Scale Instance Using count Without Destroying Existing Instance

---
### Current Situation
```
resource "aws_instance" "web" {                    
  ami                    = "ami-0220d79f3f480ecf5" 
  vpc_security_group_ids = ["sg-0db8dd8eea4a276dd"]
  instance_type          = "t2.micro"
  tags = {
    name = "TASK-9"
  }
}
```
### Backup Terraform State
```
cp terraform.tfstate terraform.tfstate.backup
```
### Modify your resource
```
resource "aws_instance" "web" {                    
  count                  = 5
  ami                    = "ami-0220d79f3f480ecf5" 
  vpc_security_group_ids = ["sg-0db8dd8eea4a276dd"]
  instance_type          = "t2.micro"
  tags = {
    name = "TASK-9"
  }
} 
```
### moving existing instance into index 0
```
terraform state mv aws_instance.web aws_instance.web[0]
```
No infrastructure changes happen — only state file changes.
### Verify Plan
```
terraform plan
```
### Apply changes
```
terraform apply -auto-approve
```
### Expected results
```
No changes to existing instance
4 new instances to be created ([1], [2], [3], [4])
No destroy action for [0]
```
