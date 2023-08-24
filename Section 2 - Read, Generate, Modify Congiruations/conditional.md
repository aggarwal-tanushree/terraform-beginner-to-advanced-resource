## Conditional Expression

### conditional.tf

```sh

provider "aws" {
    profile = "terraform"
    region = "eu-central-1"

}


variable "instance_is_dev" {}

resource "aws_instance" "dev_instance" {
    ami = "ami-0c4c4bd6cf0c5fe52"
    instance_type = "t2.micro"
    count = var.instance_is_dev == true ? 1 : 0

}

resource "aws_instance" "prod_ins" {
    ami = "ami-0c4c4bd6cf0c5fe52"
    instance_type = "t2.large"
    count = var.instance_is_dev == false ? 1 : 0
  
}

```

### terraform.tfvars

```sh
instance_is_dev = true
```
