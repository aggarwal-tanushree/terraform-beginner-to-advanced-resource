## This snippet is from the Count and Count Index video.

### iam-count-parameter.tf

```sh

provider "aws" {
    region = "eu-central-1"
    profile = "terraform"
}

variable "name_list" {
    type = list
    default = ["user-1" , "user-2" , "user-3"]

}
resource aws_iam_user "usr"{
    name = var.name_list[count.index]
    count = 3

}
```
### count-paremeter.tf

```sh

provider "aws" {
    region = "eu-central-1"
    profile = "terraform"
}


resource "aws_instance" "instance-1" {
   ami = "ami-082b5a644766e0e6f"
   instance_type = "t2.micro"
   count = 3
}
```
