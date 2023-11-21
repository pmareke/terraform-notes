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

- **Input** Variables serve as parameters for a Terraform module.
    - Each input variable accepted by a module must be declared using a `variable` block.
    - Terraform CLI defines the following optional arguments for variable declarations:
        - default - A default value which then makes the variable optional.
        - type - This argument specifies what value types are accepted for the variable.
        - description - This specifies the input variable's documentation.
        - validation - A block to define validation rules, usually in addition to type constraints.
        - sensitive - Limits Terraform UI output when the variable is used in configuration.
        - nullable - Specify if the variable can be null within the module.
    - Once a input variable is declared, you can reference it in expressions as `var.<NAME>`.
- **Output** Values are like return values for a Terraform module.
    - Output values make information about your infrastructure available on the command line,
     and can expose information for other Terraform configurations to use
    - Each output value exported by a module must be declared using an `output` block.
    - `output` blocks can optionally include `description`, `sensitive`, and `depends_on` arguments.
- **Local** Values are a convenience feature for assigning a short name to an expression.
    - A local value assigns a name to an expression, so you can use the name multiple times within a
     module instead of repeating the expression.
    - A set of related local values can be declared together in a single `locals` block.
    - Once a local value is declared, you can reference it in expressions as `local.<NAME>`.

### Modules

- A module is a container for multiple resources that are used together.
- Every Terraform configuration has at least one module, known as its root module,
 which consists of the resources defined in the .tf files in the main working directory.
- Modules can be called multiple times.
- To call a module means to include the contents of that module into the configuration with
 specific values for its input variables.
- Modules are called from within other modules using `module` blocks.
- All modules require a source argument.
    - Its value is either the path to a local directory containing the module's configuration files,
     or a remote module source that Terraform should download and use.

### Checks

- The `check` block can validate your infrastructure outside the usual resource lifecycle.
- Check blocks execute as the last step of a plan or apply after Terraform has planned or
 provisioned your infrastructure.
- Check blocks validate your custom assertions using `assert` blocks.

### Expresions

- Expressions refer to or compute values within a configuration.
- The result of an expression is a value.
    - All values have a type.
- The valid types in Terraform are `string`, `number`, `bool`, `list`, `set`,`map` and `null`.

### State

- This state is stored by default in a local file named `terraform.tfstate`.
- Terraform uses state to determine which changes to make to your infrastructure.
- Terraform provides the terraform state command to perform basic modifications of the state using the CLI.
- State snapshots are stored in JSON format.

### Tests

