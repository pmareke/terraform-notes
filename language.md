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

### Arguments

- An argument assigns a value to a particular name.
- The identifier before the equals sign is the argument name, and the expression after
 the equals sign is the argument's value.
- The context where the argument appears determines what value types are valid.

### Blocks

- A block is a container for other content.
- A block has a type.
- Each block type defines how many labels must follow the type keyword.
- A particular block type may have any number of required labels, or it may require none.
- After the block type keyword and any labels, the block body is delimited by the { and } characters.

### Identifiers

- Argument names, block type names, and the names of most Terraform-specific constructs like resources,
 input variables, etc. are all identifiers. 

### Comments

- The `#` single-line comment style is the default comment style and should be used in most cases.


### Style Conventions

- To enforce these conventions automatically run `terraform fmt`.

## Resources

- Resources are the most important element in the Terraform language.
- Each resource block describes one or more infrastructure objects.
- A resource block declares a resource of a specific type with a specific local name.

### Resource Types

- Each resource is associated with a single resource type.
- A provider is a plugin for Terraform that offers a collection of resource types.
- Each resource type is implemented by a provider.
- Based on a resource type's name, Terraform can usually determine which provider to use.
- Most of the arguments within the body of a resource block are specific to the selected resource type.
- Every Terraform provider has its own documentation, describing its resource types and their arguments.
- You can use `precondition` and `postcondition` blocks to specify assumptions and guarantees about
 how the resource operates.
- Some resource types provide a special timeouts.

### Meta Arguments

- Use the `depends_on` meta-argument to handle hidden resource or module dependencies that Terraform
 cannot automatically infer.
- If a resource or module block includes a `count` argument whose value is a whole number,
 Terraform will create that many instances.
- If a resource or module block includes a `for_each` argument whose value is a map or a set of strings,
 Terraform creates one instance for each member of that map or set.
- The `provider` meta-argument specifies which provider configuration to use for a resource.

### Data Sources

- Data sources allow Terraform to use information defined outside of Terraform.
- A data source is accessed via a special kind of resource known as a data resource,
 declared using a `data` block.
- The data source and name together serve as an identifier for a given resource and so
 must be unique within a module.

### Providers

- Terraform configurations must declare which providers they require so that Terraform
 can install and use them.
- Each provider adds a set of resource types and/or data sources that Terraform can manage.
- Every resource type is implemented by a provider.
- The Terraform Registry is the main directory of publicly available Terraform providers.

### Variables and Outputs
