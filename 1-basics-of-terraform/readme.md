### Terraform Architecture

Terraform binary is a sotware which two input

- state file (current infrastructure state)
- desired state  configuration (.tf files)

and uses plugins
- providers and provisoners
https://dev.to/techworld_with_nana/terraform-simply-explained-m
### HOW TERRAFORM WORKS

https://www.terraform.io/docs/extend/how-terraform-works.html

example aws, azure, gcp and more provider.

Use above terraform binary works.

Example
provider aws have many resources like ec2 and many others.
https://registry.terraform.io/providers/hashicorp/aws/latest/docs

Basically providers either have **resources** -> like ec2 or dataSource

resources -> used to provision resources.
example
```
# usualy syntax
resource "aws_instance" "web" {

  ami           = "xyz"
  instance_type = "t3.micro"
}
```

**data source** -> use to query resources.

```
# Lets say there are different ami id for ubuntu for different region.
data "aws_ami" "ubuntu" {
  most_recent = true

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"]
  }

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }

  owners = ["099720109477"] # Canonical
}
```
now the above can be used data.aws_ami.ubuntu.id at place of amiids


### Resources

Each resource require arguments .
some arguments are required and some are optional.
like ami-id is required.

### Provider vs Plugins

**All Providers and Provisioners used in Terraform configurations are plugins**.


Proivders need authentication.


## Terraform init

Downloads the required pluign in 
```/.terraform/plugins/<ostype>/<pluginbinary>```


## Terraform plan and apply command

# RESOURCE INDENTIFICATION.
- <resource_name>.<user_givenname>
example aws_ec2.myec2


## terraform destory
destroy existing resources.
example -> terraform destroy -target aws_ec2.myect
or just comment out in desired state.
References
- https://dev.to/techworld_with_nana/terraform-simply-explained-m