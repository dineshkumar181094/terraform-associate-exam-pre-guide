# Terraform Commands

# Terraform Init
Initialize a new or existing Terraform working directory by creating
  initial files, loading any remote state, downloading modules, etc.

  This is the first command that should be run for any new or existing
  Terraform configuration per machine. This sets up all the local data
  necessary to run Terraform that is typically not committed to version
  control.

  This command is always safe to run multiple times. Though subsequent runs
  may give errors, this command will never delete your configuration or
  state. Even so, if you have important information, please back it up prior
  to running this command, just in case.

  If no arguments are given, the configuration in this working directory
  is initialized.

NOTE -> 
- terraform cloud always encrypts the file at rest and protect it in transit with tls and also maintains the history of state changes.

## Features of terraform cloud
- single sign-on
- audting
- clustering
- private data center networking

## Terraform plan
Generate the plan

