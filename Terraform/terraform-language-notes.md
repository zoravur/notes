_**Note**: This document was written using version 1.12.x of the terraform language._

- Terraform's language is its primary user interface (the code in infra-as-code).
- Configuration files you write tell Terraform what:
	- plugins to install
	- infrastructure to create
	- data to fetch
	- and, define dependencies between resources.
- There is also block inheritance (!?)[^1]
### About the Terraform Language
- A _terraform configuration_ is a collection of files in the Terraform language[^2] that tells Terraform how to manage a given collection of infrastructure.
- The central purpose of the terraform language is to make the process of defining _resources_ as convenient and flexible as possible. Therefore, we'll start with introducing the `resource` block, along with some general syntax.
```hcl
resource "aws_vpc" "main" {
  cidr_block = var.base_cidr_block
}

<BLOCK_TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>" {
  # Block body
  <IDENTIFIER> = <EXPRESSION> # Argument
}
```
- _Blocks_ are containers for other content and usually represent the configuration of some kind of object, like a resource. Blocks have a _block type,_ can have zero or more _labels,_ and have a _body_ that contains any number of arguments and nested blocks. Most of Terraform's features are controlled by top-level blocks in a configuration file.
- _Arguments_ assign a value to a name. They appear within blocks.
- _Expressions_ represent a value, either literally or by referencing and combining other values. They appear as values for arguments, or within other expressions.




[^1]: "Terraform language also lets you define dependencies between resources and create multiple similar resources from a single configuration block." https://developer.hashicorp.com/terraform/language

[^2]: **Note:** "Terraform's configuration language is based on a more general language called HCL" https://developer.hashicorp.com/terraform/language/syntax/configuration
