# Modules 
modules helps us to keep our terraform code dry and maintainable
instead of giving full resoruce defination at one place we can have central place for module and use the those module to spin-up the resources.

convetional approach
```sh
- module
  - a
  - b
- env
  - prod
  - dev
  - uat
```
so the moduel will be at central place in modules folder and all the env refer to module

example of ec2 module
```sh
module -> 
folder ec2  -> 
main.tf ->
resources "aws_instance" "main" {
  attribute
}

module "abc" {
  source = "../modulepath"
  atrriubtes = 
}

now use this module anywhere
```

Note you need to execute terraform init command to download module or initilize modules.

## Challenges with modules
passing input to module or some sort of customization.

solution take input in module and instead of hardcoding use vars in module and pass those vars in module to

use input variable in module in short

## output in modules 
very important
when you want to display or output of module in some other module you need to use output in module.

```sh
resource "myec2" {
  module = "../modue/ec2"

}
#if you want to refer myec2 module attribute  in some other module like elastic ip moduel it is not possible directely
for that you need to have output in ec2 module
like 
# in module's ouptut section
output instance_ip {
  value = aws_instance.main.instance_id
}
and use 
module.myec2.instance_ip to refer this on parent modules namespace

```

## Terraform registery

there are many modules available on internet can be found at registory.terraform.io

tick marked are the offical one.

## Sources for module
- Local paths
- Terraform registry
- Github
- bitbucket
- Murcuraial
- Https urls
- S3 buckets
- GCS buckets

##################
 - git module
  - source = "git:https://example.vpc.git"
  - source = "git:ssh://unamepassowrd.git"
refering a branch by default branch is referd by HEAD
override it by using ref
absavd?ref=v1.2.3

downlaod module will be stored in ./teraform/moduels

## Terraform workspace
terraform allow us to have multiple workpsace, with each workpace have its different environment variables.

command
```sh
terraform workspace list # list all ws
terraform workspace new <workpsace name> 
terraform workspace show # current workspace
```
a new directory will be created terraform.tfstate.d\
inside that many workspace will be present
all states are mainted differently

## Public vs Private module registery
Important ->

### Private module registry

Private registry modules have source strings of the form <HOSTNAME>/<NAMESPACE>/<NAME>/<PROVIDER>. This is the same format as the public registry, but with an added hostname prefix.
This is the same format as the public registry, but with an added hostname prefix.

private registory can be hosted on terraform.io for an example
```sh
module "vpc" {
  source = "app.terraform.io/example_corp/vpc/aws"
  version = "0.9.3"
}
```

### Public module registry

Module Name convetion terraform-<PROVIDER>-<NAME>.
terraform-aws-ec2-instance
tag symentics x.y.z tags for releases
