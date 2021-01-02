# TERRAFORM STATE FILE
when working in large team terraform source should be put in version control system like git.
Avoid having terraform state file in vcs because it can have sensitve information in unmasked form.


.gitingore for terraform repos
- .terraform/*
- terraform.tfvars
- terrraform.tfstate
crash.log


## Remote backend

using s3 as backend
```sh
teraform {
  backend "s3" {
    bucket 
    config full
  }
}

```
partial configuration
```sh
terraform {
  backend "s3" {

  }
}
```
while init pass rest parameter

Types of backend
- standard backend -> state store and locking
- Enhanced backend -> All feature of standards + remote managment

**NOTE ->When using remote state, state is only ever held in memory when used by Terraform. It may be encrypted at rest, but this depends on the specific remote state backend.**
Sate will never come up as a file in local machine, it will be only kept in ram for operation.
This prevention is strictly applied post terraform v0.9
## Statefile locking
Whenever you are performing wirte ops, terraform would lock the statefile.
This is very important otherwise during your ongoing terraform apply operation, if some others allso tries the same, it would corrupt your statefile

Note -> by default locking feature is not present in s3

**we can use dynamodb_table attribute to performe locking feature**
**To use DynamoDB for locking with Terraform, you must create a DynamoDB table with a primary key called ``LockID`` with this exact spelling and capitalization**


## Terraform state managment
it is recommended that you never modify terraform state manually be editing file always recommend to use cli commands

commands available 
```sh
list -> list the resorces in statefile 
  terraform list 
mv -> move item in terrform state (renaming existin resrouces)
 terraform mv aws_instance.ec2 aws_instance.myec2
 #This command can also move to a destination address in a completely different state file
 
pull -> manually download and output state
  terraform pull
push -> pushes the state manually
 terraform push 
rm -> remove resources from state file
  terraform rm aws_instance.ec2
  next time when we plan it will recrate it
show -> show the attributes of single 
resources
  terraform show 
  terraform show aws_instance.myec2
```


## Importing existing resources in terraform
manual resource then you need to manage it by terraform.

Note -> it will only generate statefile not the desired state you need to write .tf files for desired state accordingly

example we need to import aws instance then
```sh
terraform import aws_instance.myec2 <instance-id>

```
**NOTE -> command currently can only import one resource at a time**
will get instance in state file
