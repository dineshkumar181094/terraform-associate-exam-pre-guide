# Terraform State File.

Most important concept in terraform is its statefile how terraform manages.
by default terraform will create 
```terraform.tfstate```

in current working directory it is like a database which tells terraform which resources it is managing.
lame example -> if you have crated instance how do terraform comes to know which resource it is managin because of state file.

example of statefile
```sh
{
      "mode": "managed",
      "type": "aws_s3_bucket",
      "name": "s3bucket",
      "provider": "provider.aws",
      "instances": [
        {
          "schema_version": 0,
          "attributes": {
            "acceleration_status": "",
            "acl": "private",
            "arn": "arn:aws:s3:::learnandplaysabkuch",
            "bucket": "learnandplaysabkuch",
            "bucket_domain_name": "learnandplaysabkuch.s3.amazonaws.com",
            "bucket_prefix": null,
            "bucket_regional_domain_name": "learnandplaysabkuch.s3.ap-south-1.amazonaws.com",
            "cors_rule": [],
            "force_destroy": false,
            "grant": [],
            "hosted_zone_id": "Z11RGJOFQNVJUP",
            "id": "learnandplaysabkuch",
            "lifecycle_rule": [],
            "logging": [],
            "object_lock_configuration": [],
            "policy": null,
            "region": "ap-south-1",
            "replication_configuration": [],
            "request_payer": "BucketOwner",
            "server_side_encryption_configuration": [],
            "tags": {},
            "versioning": [
              {
                "enabled": false,
                "mfa_delete": false
              }
            ],
            "website": [],
            "website_domain": null,
            "website_endpoint": null
          },
          "private": "bnVsbA=="
        }
```

The above file has all the information about terraform.

## Terraform state referesh
- Whenever we run terraform plan terraform refresh the state by hitting aws api to get the current state of the infrastructre that is why sometimes people call it current state also.

now that state is being compared with desired state and plan is genrated accordingly.
Terraform will always push towards desired state.

```command - terraform refresh ```

## Terraform show 
display the content of state file

``` command - terrafrom show ```

Terraform fetches the current state by doing terraform refresh and then displaay the diff between current state and desried state.




## Reference
- https://www.terraform.io/docs/state/index.html