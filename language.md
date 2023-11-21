# [Terraform Language Documentation](https://developer.hashicorp.com/terraform/language)

- Configuration files you write in Terraform language tell Terraform what plugins to install,
 what infrastructure to create, and what data to fetch.
- Terraform language also lets you define dependencies between resources and create multiple
 similar resources from a single configuration block.
- The main purpose of the Terraform language is declaring resources, which represent infrastructure objects.
- A configuration can consist of multiple files and directories.
- The Terraform language is declarative, describing an intended goal rather than the steps to reach that goal.

The syntax of the Terraform language consists of only a few basic elements:

```terraform
<BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>" {
  # Block body
  <IDENTIFIER> = <EXPRESSION> # Argument
}
```
- Blocks are containers for other content and usually represent the configuration of some kind of object,
 like a resource.
- Arguments assign a value to a name. They appear within blocks.
- Expressions represent a value, either literally or by referencing and combining other values.

## Files and Directories

- Code in the Terraform language is stored in plain text files with the `.tf` file extension.
- A module is a collection of .tf files kept together in a directory.
- Nested directories are treated as completely separate modules,
 and are not automatically included in the configuration.
- Terraform evaluates all of the configuration files in a module,
 effectively treating the entire module as a single document
 - A Terraform module can use module calls to explicitly include other modules into the configuration.
 - These child modules can come from local directories or from external sources like the Terraform Registry.
 - Terraform always runs in the context of a single root module.
    - In Terraform CLI, the root module is the working directory where Terraform is invoked.
- If two files attempt to define the same object, Terraform returns an error.
- Terraform has special handling of any configuration file whose name ends in `_override.tf`.
- Terraform initially skips these override files when loading configuration, and then afterwards processes each one.
- Use override files only in special circumstances.

## Syntax
