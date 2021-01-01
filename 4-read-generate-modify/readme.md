## Outputs

Terraform has the capablites to output the attribute of a resource with output values.

Output attribute from one resources not only used for user interface but also can act as input to other resources as well.


example -> 
```sh
resource "aws_ip" "lb" {
  vpc = true
}
output "eip" {
  value = aws_eip.lb.public_ip
}
```
when we apply the above configuration it will disply output directly onto the screen.
we can refer attribute reference section of a particular resource check for the documentation.


## Cross Resrouce references
we can refer attribute of one resource in other resources.

example

```sh
resource "aws_instance" "myec2" {
   ami = "ami-082b5a644766e0e6f"
   instance_type = "t2.micro"
}

resource "aws_eip" "lb" {
  vpc      = true
}

resource "aws_eip_association" "eip_assoc" {
  instance_id   = aws_instance.myec2.id #refring 
  allocation_id = aws_eip.lb.id #refering
}
```

## Important 
in version 11 -> "${aws_instance.myec2.id}" this style was used
in version 12 -> aws_instance.myec2.id
direct usage
but if you want to conactenate string still need to use 11 version

## Terraform variables.

Variable makes terraform scalable and mantainble instead of hardocding value we can use the varibles.
and refer them whereever require.

Multiple ways of assigning value to variable.
 - Environment variables.
    - TF_VAR_{variable}
 - Commandline flag.
    - terraform -var 'foo=bar'
 - From file.
    - terraform.tfvars or terraform.tfvars.json
    - anyfile.auto.tfvars or anyfile.auto.tfvars.json
    - -var-file=custom.tfvars
 - Variable default
    - default value in decleration.
and if no value is given then terraform will promt to user to ask value.


## Data Type for Variables.
Note -> if no type is defined variable can accept any data type.
```sh
variable <var_name> {
  type = "string"
  default = "dinesh"
}
```
variable argument
- description
- type
- defaut
- validation
- sensitive

datatype in terrafrom
- string
- number
- bool

- list
  - access list iterm var.<var_name>[index]
- set
- map
  - access var.<var_name>["key_name"]
- object
- tuple

## Count parameter and resources

Some sort of for loop
```sh
resources "aws_iam_user" "user" {
  name = "user-number-${count.index}"
  count = 5
# index is important form examp point of view
}
```


## Conditional expresion 
```sh
condition ? true_val : false_false
count = var.istest == true ? 1 : 0
# if istest is true the count becomes true
else become false
```

## local values
A local value assigns a name to expression, allowing it to be used mutlitple times within a module without repeating it.

```sh
locals {
  common_tags = {
    owner = "devops"
    service = "backend"
  }

resources "aws_instance" "bac" {
  ami = "ami-d"
  tags = local.common_tags
}
# local values can be sued for different use-cases like having a conditional expression

locals {
  name_prefix = "${vaar.name != "" ? var.name : var.default}"
}

# now use local.name_prefix everywhere
}
```

## Function in terraform
The terraform laungage includes a number of built-in fuction that can be used to transform and combine values.

syntax -> function(arg1,arg2)
Note -> terraform doesn't support user defined functions.

example function 
```sh

lookup(map, key, default) # lookup map
element([list], index)  # get element from list
file(path) # loads the content of file
```

## Data sources.

performs data query on aws resources.
example fetch ami-id make query on aws amis.
```sh
data "aws_ami" "myami" {
  query = attribute
}

now use as data.aws_ami.myami
```

## Debugging terraform

Environment variable TF_LOG
and want in file then use env var
TF_LOG_PATH= ./xyz.log
can be set to 
- TRACE (most verbose)
- DEBUG
- INFO
- WARN
- ERROR


## Terraform fmt
formats the file in clear way

terraform fmt 

## Terraform validate command
- Terraform validate primary check wheatres a configuration systactically correct or not, 
any unsuportted argument or undefined variables.

## Dynamic Blocks


## Taint Resource
The terraform taint command manually marks a terraform-managed resources as tainted, forcing it to be destoryed and recreated on the next apply.

```sh
resource "aws_instance" "xyz" {

}
terraform taint aws_instance.xyz
# in state file it will show tainted in status.
# when ever there is lot of changes the resources can be tainted.
```


## Splat Expression
splat expression used to get list of all the attributes.

```sh
resources "xyz" "main"  {
  name = "asdf"
  count = 3
}
output "arns" {
  value = aws_iam_user.main[*].arn
}
```

## Terraform graph
Generate visual represntation of either a config or plan 
it can also show the dependicies.

Output in dot format.

## Saving Terraform plan to file

terraform plan -out=tmp.txt

## Terraform outputs
TO get the output of value on cli

```sh
terraform output variabl_name
```

## Terraform settings

special terraform configuration block type is used tto configure some behaviours of terraform itself, such as requring minimum version of terraform to apply configuration.
```sh
terraform {
 required_version = "11.04"
}
```
provider version in this block
```sh

terraform {
 required_version = "11.04"
 required_providers {
  aws = "~> 2.0"
}
}
Note -> from 12 version of terraform it is required to provider's version in terraform block
```

## Delaing with larger infrastructure.
when you have larger infrastructure, you will face issue related to API limits for providres.

Whenver terraform plan command is happen it will refersh state to get current state will run api limits

you can use
``` refresh=false ```
while planing
or you can target a particular module
```-target aws_instance.main```
## Reference
https://www.terraform.io/docs/configuration/variables.html