# Lab: HashiCorp Configuration Language

Terraform is written in HCL (HashiCorp Configuration Language) and is designed to be both human and machine
readable. HCL is built using code configuration blocks which typically follow the following syntax:

```hcl
# Template
<BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>" {
 # Block body
<IDENTIFIER> = <EXPRESSION> # Argument
}

# AWS EC2 Example
resource "aws_instance" "web_server" { # BLOCK
  ami = "ami-04d29b6f966df1537" # Argument
  instance_type = var.instance_type # Argument with value as expression (Variable value replaced 11 }
```

when you're writing code with Terraform, you organize your instructions into different blocks. Here's a brief explanation of each type:

1. **Terraform Settings Block:**
   - This is where you configure settings for your entire Terraform configuration, such as the required Terraform version.

2. **Terraform Provider Block:**
   - Here, you define the cloud or infrastructure provider you'll be working with, like AWS, Azure, or Google Cloud. It includes authentication details and other provider-specific settings.

3. **Terraform Resource Block:**
   - This block is used to define and configure a specific resource provided by the chosen provider. For example, it could be an AWS EC2 instance or an Azure storage account.

4. **Terraform Data Block:**
   - Data blocks allow you to fetch and use data from external sources, like information about an existing resource that you want to use in your configuration.

5. **Terraform Input Variables Block:**
   - Input variable blocks are where you define parameters that users can input when running your Terraform code. These variables make your code more flexible and reusable.

6. **Terraform Local Variables Block:**
   - Local variables are like temporary placeholders within your Terraform configuration. You can use them to simplify complex expressions or reuse values in multiple places.

7. **Terraform Output Values Block:**
   - Output blocks allow you to expose certain values from your Terraform configuration. These values can be useful for other parts of your infrastructure or external processes.

8. **Terraform Modules Block:**
   - Modules are a way to organize and reuse parts of your Terraform configuration. They encapsulate a set of resources and can be used across multiple projects, promoting code reusability.

In summary, these different block types in Terraform help you structure your code, manage configurations for different parts of your infrastructure, and make your code more adaptable and reusable. Each block type serves a specific purpose in defining, organizing, and managing your infrastructure as code.


We will be utilizing Terraform Provider, Terraform Resource, Data and Input Variables Blocks in this lab. This course
will go through each of these configuration blocks in more detail throughout the course.
- Task 1: Connect to the Student Workstation
- Task 2: Verify Terraform installation
- Task 3: Update Terraform Configuration to include EC2 instance
- Task 4: Use the Terraform CLI to Get Help
- Task 5: Apply your Configuration
- Task 6: Verify EC2 Server in AWS Management Console

![AWS Application Infrastructure Buildout](img/obj-2-hcl.png)


## Task 1: Connect to the Student Workstation
In the previous lab, you learned how to connect to your workstation with either VSCode, SSH, or the web-based
client.
One you’ve connected, make sure you’ve navigated to the `/workstation/terraform` directory. This is where we’ll
do all of our work for this lab.

## Task 2: Verify Terraform installation

### Step 1.2.1

Run the following command to check the Terraform version:

```hcl
terraform -version
```

You should see:
```hcl
Terraform v1.0.8
```

## Task 3: Update Terraform Configuration to include EC2 instance

### Step 1.3.1

In the `/workstation/terraform` directory, edit the file titled `main.tf` to create an AWS EC2 instance within one of the
our public subnets.

Your final `main.tf` file should look similar to this with different values:

```hcl
provider "aws" {
  access_key = "<YOUR_ACCESSKEY>"
  secret_key = "<YOUR_SECRETKEY>"
  region = "<REGION>"
}

resource "aws_instance" "web" {
  ami = "<AMI>"
  instance_type = "t2.micro"

  subnet_id = "<SUBNET>"
  vpc_security_group_ids = ["<SECURITY_GROUP>"]

  tags = {
  "Identity" = "<IDENTITY>"
  }
}
```

Don’t forget to save the file before moving on!


## Task 4: Use the Terraform CLI to Get Help

### Step 1.4.1

Execute the following command to display available commands:

```hcl
terraform -help

Usage: terraform [-version] [-help] <command> [args]

The available commands for execution are listed below.
  The most common, useful commands are shown first, followed by
  less common or more advanced commands. If you're just getting
  started with Terraform, stick with the common commands. For the
  other commands, please read the help and docs before usage.

Common commands:
  apply    Builds or changes infrastructure
  console  Interactive console for Terraform interpolations
  destroy  Destroy Terraform-managed infrastructure
  env      Workspace management
  fmt      Rewrites config files to canonical format
  get      Download and install modules for the configuration
  graph    Create a visual graph of Terraform resources
  import   Import existing infrastructure into Terraform
  init     Initialize a Terraform working directory
  output   Read an output from a state file
  plan     Generate and show an execution plan

  ...
```
(full output truncated for sake of brevity in this guide)

Or, you can use short-hand:

```hcl
terraform -h
```

### Step 1.4.2

Navigate to the Terraform directory and initialize Terraform

```hcl
cd /workstation/terraform
```

```hcl
terraform init
  Initializing provider plugins...
  ...

Terraform has been successfully initialized!
```

### Step 1.4.3
Get help on the plan command and then run it:

```hcl
terraform -h plan
```
```hcl
terraform plan
```

## Task 5: Apply your Configuration

### Step 1.5.1
Run the `terraform apply` command to generate real resources in AWS:

```hcl
terraform apply
```

You will be prompted to confirm the changes before they’re applied. Respond with `yes`.

## Task 6: Verify EC2 Server in AWS Management Console

Login to AWS Management Console -> Services -> EC2 to verify newly created EC2 instance:

![AWS EC2 Server](img/obj-2-ec2.png)

### References
[Terraform Configuration Terraform Configuration Syntax](https://developer.hashicorp.com/terraform/language/syntax/configuration)
