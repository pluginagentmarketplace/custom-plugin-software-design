---
name: infrastructure-as-code
description: Infrastructure as Code using Terraform, Ansible, and CloudFormation. Master declarative infrastructure management.
---

# Infrastructure as Code (IaC)

## Quick Start

IaC enables managing infrastructure programmatically.

### Terraform
```hcl
# Configure AWS Provider
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}

# VPC
resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  tags = { Name = "main-vpc" }
}

# Subnet
resource "aws_subnet" "main" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.1.0/24"
  availability_zone = "us-east-1a"
}

# EC2 Instance
resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t3.micro"
  subnet_id     = aws_subnet.main.id
  
  tags = { Name = "web-server" }
}

# Output
output "instance_ip" {
  value = aws_instance.web.public_ip
}
```

### Ansible
```yaml
---
- hosts: webservers
  become: yes
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start Nginx
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Deploy application
      copy:
        src: app/
        dest: /var/www/html/
```

## IaC Workflow

```
1. Write Infrastructure Code (Terraform/CloudFormation)
2. Version Control (Git)
3. Plan Changes (terraform plan)
4. Review & Approve
5. Apply Changes (terraform apply)
6. Monitor & Update
```

## Best Practices

- Version control all IaC code
- Use modules for reusability
- Implement proper state management
- Separate environments (dev, staging, prod)
- Document infrastructure decisions
- Automate testing of infrastructure
- Enable change tracking and auditing
- Implement least privilege access

## Tools

- **Terraform** - Multi-cloud, declarative
- **CloudFormation** - AWS-native
- **Ansible** - Agentless, procedural
- **Chef/Puppet** - Configuration management
- **Pulumi** - Programming language-based

## Resources

- [Terraform Docs](https://www.terraform.io/docs)
- [Ansible Docs](https://docs.ansible.com)
- [AWS CloudFormation](https://docs.aws.amazon.com/cloudformation)
