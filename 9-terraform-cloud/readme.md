# Terraform Cloud

### Terraform cloud manages runs terraform in a consistent and reliable environment with various features like access control, private registries of module sharing, policy control, cost estimation and other.

```Because of terraform cloud all team members will run the same version of terraform.```

### Important Feature of Tf Cloud
- Approval system. (add comment, discard or run)
- Same and consitent env for all devs.
- Cost estimation.
- Policy checks (sentinel).
- Many devs can comment.
- State file is stored in the tf cloud itself.
- UI for entering environment variable and terraform variables as well.
  - You can mark a variable sensivte if you don't want to display on gui.
- Private registory for modules.


### sentinal (policies)

Sentinal are the policy checks which can assoicated with a terraform run.
It is embeded policy as code framework integrated with Hashicorp Enterprise products.

It is a paid feature.
example we want instance to have tags, then we can attach to a run.

```
Policy -> Policyset -> Workspace
```
policy is attached to policy set and policyet is attached to workspace.
They can hard-mandatory, soft-manadatory, advisory

For WORKSPACE  VCS control it can be connected to
- Github
- Gitlab
- Bitbucket
- AzureDevOps



### Remote Backends
The remote backend stores terraform statefile and may be used in terraform cloud.

Terraform cloud can also be used with local operation, in which case only state is stored in the terraform cloud.


we can use terraform cloud as remote backend

```
# Using a single workspace:
terraform {
  backend "remote" {
    hostname = "app.terraform.io"
    organization = "company"

    workspaces {
      name = "my-app-prod"
    }
  }
}
```
All the operation happens in terraform cloud but all logs will be streamed from local machine
