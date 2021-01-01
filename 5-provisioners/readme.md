# Provisioner
Provisinores are used to execute scripts on a local or remote machine as part of resource creation or destruction.

Terraform has capability to turn provisioners both at the time of resrouce creation as well as desctruction.

Two type of provisioners.
- local-exec
- remote-exec

### local-exec
provisoners allow us to invoke local executable after resrouce is created.

```sh
resource " aws_instance " "web" {
  provisioner "local-exec" {
    command = "$echo "hello world"
  }
}
```

### remote-exec
this provisioners allow to invoke scripts directly on the remote server.

```sh
resource "aws_instance" "web" {
  
  provisioner "remote-exec" {
    command = "echo "hello world"
  }
}
```
### example of provisioner
- file -> copy file
- remote-exec -> exec command on remoter machine
- local-exec -> on local machine
- chef
- habitat
- puppet
- salt-masterless

## Creation time provisioner and destroy time provisioner

exmple destroy time provisioner
```sh
resource "aws_instance" "web" {

  provisioner "local-exec" {
    when = "destroy"
    command = "echo hello world"
  }
  connection { # to connect to instance

  }
}
## use inline when giving array 

inline = [
  "commmand 1",
  "command 2"
]
```
default if provisoner fails resource is marked as tainted.
you can change this behaviour by using on_fail attribute.

```sh
on_fail = contiune
```
will contiune if fails else resource will be marked as tainted.
