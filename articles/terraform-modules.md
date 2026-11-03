# Terraform Modules Explained: A Practical Guide

## 1. Introduction

When working with Terraform, we use configuration files to define and manage infrastructure as code (IaC).

For example, we might create AWS resources such as EC2 instances, VPCs, subnets, security groups, and S3 buckets.

As our infrastructure grows, managing all these resources in a single configuration can become difficult. This is where **Terraform modules** become useful.

Terraform modules allow us to organize infrastructure code into reusable and manageable components. Instead of writing the same configuration repeatedly, we can create a module once and reuse it across different projects and environments.

In this tutorial, we will explore Terraform modules, understand how they work, and build practical examples using AWS.

---

## 2. What Is a Terraform Module?

A Terraform module is a collection of Terraform configuration files (`.tf`) stored together in a directory.

It is a reusable building block for managing infrastructure.

For example, imagine you frequently need to create EC2 instances. Instead of writing the EC2 configuration from scratch every time, you can organize that configuration into a module and reuse it whenever needed.

### Module-Based Infrastructure

A Terraform project can be organized into a root module that calls multiple child modules.

For example:

```text
terraform-project/
│
├── main.tf
├── variables.tf
├── outputs.tf
│
└── modules/
    ├── ec2/
    ├── vpc/
    └── rds/
```

The root module can call the EC2, VPC, and RDS modules to manage different infrastructure components.

### Example: EC2 Module Structure

The EC2 module might have the following structure:

```text
terraform-project/
│
├── main.tf
├── variables.tf
├── outputs.tf
│
└── modules/
    └── ec2/
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
```

The `ec2` directory contains another Terraform module.

We call the first module the **root module**, and the `ec2` module a **child module** when the root module calls it.

**Important:** A Terraform module doesn't have to contain all three files (`main.tf`, `variables.tf`, and `outputs.tf`). It can consist of just one `.tf` file or multiple configuration files.

---

## 3. Root Modules vs. Child Modules

### 3.1 What Is a Root Module?

The root module is the main Terraform working directory where you run Terraform commands.

For example:

```bash
terraform init
terraform plan
terraform apply
```

Terraform uses the configuration files in your current working directory. This directory represents your root module.

Example:

```text
terraform-project/
│
├── main.tf
├── variables.tf
└── outputs.tf
```

### 3.2 What Is a Child Module?

A child module is a Terraform module that is called by another module.

For example, suppose your root module needs to create an EC2 instance. Instead of defining the EC2 resource directly in the root module, you can create a separate directory containing the EC2 configuration.

Example:

```text
terraform-project/
│
├── main.tf
├── variables.tf
├── outputs.tf
│
└── modules/
    └── ec2/
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
```

Here:

- `terraform-project` is the root module.
- `modules/ec2` is the child module.
- The root module calls the child module using a `module` block.

### 3.3 How Does the Root Module Call a Child Module?

Inside the root module's `main.tf`, we can write:

```hcl
module "ec2" {
  source = "./modules/ec2"
}
```

Let's understand each line:

| Configuration | Explanation |
|---|---|
| `module` | Tells Terraform that we are calling a module. |
| `"ec2"` | The local name we give this module instance. |
| `source` | Specifies where Terraform should find the module. |
| `"./modules/ec2"` | Relative path to our child module directory. |

**Note:** A child module does not need to be deployed independently. It is commonly called and managed through its root module.
## 4. Creating a Reusable Terraform Module
4.1 Understanding the concept
A root module can call a child module using a module block.

```hcl
module "ec2" {
  source = "./modules/ec2"
}
```

This tells Terraform where to find the child module, but it doesn't tell us what EC2 instance to create.


