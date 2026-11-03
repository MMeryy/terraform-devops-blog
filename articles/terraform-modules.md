<h><b>Terraform Modules Explained: A Practical Guide</b></h>
<br><br>
<h>1. Introduction</h><br><br>
When working with Terraform, we use configuration files to define and manage infrastructure as code (IaC) For example, we might create AWS resources such as EC2 instances, VPCs, Subnets, Security groups and S3 buckets. As our infrastructure grows, managing all these resources in a single configuration can become difficult. This is where Terraform Modules becomes useful.

Terraform modules allow us to organize infrastructure code into reusable and manageable components. Instead of writing the same configuration repeatedly, we can create a module once and reuse it across different projects and environments.

In this tutorial, we will explore Terraform modules, understand how they work, and build practical examples using AWS.

<h>2. What is a Terraform Module</h> <br><br>
A Terraform module is a collection of Terraform configuration files (.tf) stored together in a directory.
It a reusable building block of infrastructure.
For example, imagine you frequently need to create EC2 instances. Instead of writing the EC2 configuration from scratch every time, you can organize that configuration into a module and reuse it whenever needed.

    Module-Based Infrastructure

                    Root Module
                    (main.tf)
   
       EC2 Module  VPC Module  RDS Module

terraform-project/</br>
│</br>
├── main.tf</br>
├── variables.tf</br>
├── outputs.tf</br>
│</br>
└── modules/</br>
    └── ec2/</br>
        ├── main.tf</br>
        ├── variables.tf</br>
        └── outputs.tf</br>
The ec2 directory contains another Terraform modules.</br>

We call the first module the root module, and the ec2 module a child module when the root module calls it.

Important: A Terraform module doesn't have to contain all three files. It can consist of just one .tf file or multiple configuration files.

<h>Section 3: Root Modules vs. Child Modules</h><br><br>
<h>1. What is a root module?<h><br>
   The root module is the main Terraform working directory where you run Terraform commands.
   For example, when you execute -
   terraform init, terraform plan and terraform apply 

   Terraform uses the configuration files in your current working directory. The directory represents your root module. 

    terraform-project/</br>
    │</br>
    ├── main.tf</br>
    ├── variables.tf</br>
    └── outputs.tf</br>
<br>
<h>2. What is a child module?</h><br><br>
A child module is a Terraform module that is called by another module.

For example, suppose your root module needs to create Ec2 instance. Instead of defining the EC2 resource directly in the root module, you can create a separate directory containing the EC@ configuration. 


