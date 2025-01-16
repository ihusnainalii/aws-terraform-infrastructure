# AWS Terraform Infrastructure

This repository contains Terraform configurations for setting up an AWS infrastructure environment with modularized components. The infrastructure includes a VPC, subnets, internet gateway, NAT gateway, route tables, security groups, and an Application Load Balancer (ALB).

## Project Structure

```plaintext
.
├── README.md
└── terraform
    ├── environments
    │   ├── dev
    │   │   ├── main.tf             # Main Terraform configuration for the dev environment
    │   │   ├── provider.tf         # AWS provider and backend configuration
    │   │   ├── terraform.tfvars    # Environment-specific variable values
    │   │   └── variables.tf        # Variables for the dev environment
    │   └── prod
    │       ├── main.tf             # Main Terraform configuration for the prod environment
    │       ├── provider.tf         # AWS provider and backend configuration
    │       ├── terraform.tfvars    # Environment-specific variable values
    │       └── variables.tf        # Variables for the prod environment
    └── modules
        ├── alb.tf                  # ALB resource configurations
        ├── outputs.tf              # Output values for reusable information
        ├── security_groups.tf      # Security group configurations
        ├── variables.tf            # Module-level variables
        └── vpc.tf                  # VPC and subnet configurations
```

## Infrastructure Overview

This project sets up the following AWS resources:

* **VPC**: A dedicated network environment for your infrastructure.
* **Subnets**: Public and private subnets in multiple availability zones.
* **Internet Gateway**: Provides internet access for public subnets.
* **NAT Gateway**: Allows private subnets to access the internet securely.
* **Route Tables**: Manages routing for public and private subnets.
* **Security Groups**: Restricts access to resources at the network level.
* **Application Load Balancer (ALB)**: Distributes incoming traffic across targets in public subnets.

## Environments

* `dev`: Development environment configuration.
* `prod`: Production environment configuration.

## Modules

The infrastructure is modularized for reusability and better organization:

* `vpc.tf`: Manages the creation of VPC, subnets, and route tables.
* `security_groups.tf`: Configures security groups.
* `alb.tf`: Sets up an Application Load Balancer (ALB).
* `outputs.tf`: Defines reusable outputs.
* `variables.tf`: Defines inputs for module parameters.


## Variables

The following variables must be defined in `terraform.tfvars` for each environment:

```plaintext
Variable Name       Description                     Example
-------------       -----------                     -------
environment         Environment name                dev or prod
aws_region          AWS region                      us-east-1
vpc_cidr            VPC CIDR block                  10.0.0.0/16
availability_zones  List of availability zones      ["us-east-1a", "us-east-1b"]
```

## Prerequisites

1. Install Terraform.
2. Set up AWS credentials with the necessary permissions.
3. Update `terraform.tfvars` with appropriate values for each environment.

## Getting Started

1. Clone this repository:
```bash
git clone <repository-url>
```

2. Navigate to the project directory:
```bash
cd <project-directory>
```

3. Initialize Terraform:
```bash
terraform init
```

4. Review the planned changes:
```bash
terraform plan
```

5. Apply the infrastructure:
```bash
terraform apply
```

# Important Notes

* Always review the planned changes before applying them.
* Keep your AWS credentials secure and never commit them to version control.
* Monitor AWS costs regularly to avoid unexpected charges.

# Contributing

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

# License