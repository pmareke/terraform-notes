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
