# [Terraform CLI Documentation](https://developer.hashicorp.com/terraform/cli)

## Initializing Working Directories

- `terraform init` initialize a working directory that contains a Terraform configuration.
- `terraform get` download modules referenced in the configuration.

## Provisioning Infrastructure 

- `terraform plan` evaluates a Terraform configuration to determine the desired state of all the
 resources it declares, then compares that desired state to the real infrastructure objects
 being managed with the current working directory and workspace.
- `terrafrom apply` performs a plan just like terraform plan does, but then actually carries out
 the planned changes to each resource.
- `terraform destroy` destroys all of the resources being managed by the current working directory and workspace.

## Writing and Modifying Terraform Code

- `terraform console` starts an interactive shell.
- `terraform fmt`  rewrites Terraform configuration files to a canonical format and style.
- `terraform validate` validates the syntax and arguments of the Terraform configuration files in a directory.

## Inspecting Infrastructure

- `terraform graph` creates a visual representation of a configuration or a set of planned changes.
- `terraform output` can get the values for the top-level output values of a configuration.
- `terraform show` can generate human-readable versions of a state file or plan file.
- `terraform state list` list the resources being managed by the current working directory and workspace.
- `terraform state show` can print all of the attributes of a given resource being managed by the
 current working directory and workspace.

## Testing Terraform

- `terraform test` reads in Terraform testing files and executes the tests within..
