The `terraform {}` block configures terrafrom itself, including which providrers to install, and which version of Terraform to use to provision your infrastructure.

In general, it is recommended to use multiple, composable terraform files for maintainability; therefore, it is suggested to put the terraform block inside a `terraform.tf` file.

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.92"
    }
  }

  required_version = ">= 1.2"
}
```

