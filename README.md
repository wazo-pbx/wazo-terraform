# xivo-aws

Install terraform (http://terraform.io)

Create a xivo.tf with this content:

```
provider "aws" {
    access_key = ""
    secret_key = ""
    region = "us-east-1"
}

resource "aws_instance" "xivo" {
    ami = "ami-8b9a63e0"
    instance_type = "t2.micro"
    subnet_id = ""
    key_name = ""

    provisioner "remote-exec" {
        inline = [
        "wget --no-check-certificate https://raw.githubusercontent.com/sboily/xivo-aws/master/xivo_install_aws",
        "sudo bash /home/admin/xivo_install_aws"
        ]

        connection {
            user = "admin"
            private_key = ""
        }
    }
}
```

Update with your value:

- access_key
- secret_key
- subnet_id
- key_name
- private_key

Launch this command:

    terraform plan
    terraform apply

At this end:

    terraform show
    
To remove instance:

    terraform plan -destroy
    terraform destroy
    
Have fun!
