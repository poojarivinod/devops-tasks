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
