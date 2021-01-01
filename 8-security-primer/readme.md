# Security
it is not recommend to hard-code creds in terraform vcs there are different ways to auth will be discussed below.

## AWS provider auth
can use environment variable of aws cli for auth

## Deploying Resources in mutiple region 
lets say there are two ec2 instance 

direct scenario 
eip1 -> mumbai
eip2 -> ohio
```sh
# alias will help us to have multiple configuration for same provider
provider "aws" {
  region ="ap-south-1"

}
provider "aws" {
  region = "us-west-2"
  alias = "ohio"
}

resource "aws_eip" "myeip" {
  vpc = true
  provider = "aws.ohio" # important to use alias
}
```

## Handeling multiple aws profile with terraform providers

use profile parameters

```sh
provider "aws" {
  region ="ap-south-1"
  profile = "account1"

}
provider "aws" {
  region = "us-west-2"
  alias = "ohio"
  profile = "account2"
}
```

