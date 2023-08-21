### Documentation Referred:

https://registry.terraform.io/providers/hashicorp/aws/2.42.0/docs/resources/eip

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group

### reference-attributes.tf

```sh
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "~> 5.0"
    }
     /* github = {
      source = "integrations/github"
    }*/
  }
}

provider "aws" {
    region = "eu-central-1"
    profile = "terraform"
}

resource "aws_eip" "eip" {
  domain = "vpc"

  tags = {
    Name = "iac_eip "
  }
}

resource "aws_security_group" "allow_tls" {
  name = "allow_tls1"
  description = "Allows TLS inbound traffic"

  ingress {
    description = "TLS for default VPC"
    from_port   = 443
    to_port =   443
    protocol =  "tcp"
    cidr_blocks  = ["${aws_eip.eip.public_ip}/32"] 
  }

  egress {
    from_port = 0
    to_port = 0
    protocol = "-1"
    cidr_blocks = ["0.0.0.0/0"]
    description = "all outbound"

  }

  tags = {
    Name = "allow_tls_sg"
  }
}


```

### Commands Used:
```sh
terraform plan
terraform apply
terraform apply -auto-approve
terraform destroy -auto-approve
```
