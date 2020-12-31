# Terraform Provider
Terraform provider is part of plugin there are different provider in terraform.
They are just simple go binaries which calls the apis of the clouds.

During init, if version argument are not specified, the most recent provider will be downloaded during initizating.

It is highly recommended to specify the version of provider you want in terraform config.

** NOTE - A config can have multiple provider  **
** location of provider /.terraform/plugins/<ostype>/<provider_binary> **


```
provider "aws" {
  region = "ap-south-1"
  version = "2.7"
}
```

| provider version | meaning|
| ------------- | ------------- |
| >=1.0          | greater than equ 1.0|
| <=1.0   | less than equ 1.0  |
| ~> 2.0  | any version 2.x |
| >=2.3 , <2.5 | between these number


## Types of provider
- Harshicorp distrubuted.
    - downloaded automatically when terraform init is done.
- 3rd party provider
  - when existing provider doesn't solve the usecase or you want build some custom

Note -> 3rd party plugin won't be downloaded directly they need to be put in specific directory.

- ~/.terraform/plugins

