## Local Values example.

### local-values.tf

```sh
provider "aws" {
    profile = "terraform"
    region = "eu-central-1"
}

locals {
    common_tags = {
        dept = "DevOps"
        env = "test"
    }
}

resource "aws_instance" "dev_instance" {
  ami = "ami-0c4c4bd6cf0c5fe52"
  instance_type = "t2.micro"
  tags = local.common_tags
}

resource "aws_ebs_volume" "db_ebs" {
  availability_zone = "eu-central-1a"
  size = 8
  tags = local.common_tags
}
```
