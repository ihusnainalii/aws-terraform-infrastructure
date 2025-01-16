# Terraform Infrastructure Workflow

This GitHub Actions workflow automates the deployment and destruction of Terraform infrastructure in AWS.

## Workflow Trigger

The workflow triggers on the following events:
- **Push**: To the `main` or `aws-terraform-infra` branches.
- **Pull Request**: Against the `main` or `aws-terraform-infra` branches.
- **Manual Trigger**: Via `workflow_dispatch` with the following input:


    action: (required)

        apply: Deploy the infrastructure.
        destroy: Remove the infrastructure.




## Permissions

The workflow requires the following permissions:
- **id-token**: Write access
- **contents**: Read access

## Jobs

### 1. `terraform-apply`
- **Condition**: Runs when the `action` input is `apply`.
- **Steps**:
- Check out the repository.
- Configure AWS credentials using the provided IAM role.
- Set up Terraform with version `1.5.0`.
- Initialize Terraform (`terraform init`).
- Generate and display an execution plan (`terraform plan`).
- Apply the Terraform configuration (`terraform apply -auto-approve`).

### 2. `terraform-destroy`
- **Condition**: Runs when the `action` input is `destroy`.
- **Steps**:
- Check out the repository.
- Configure AWS credentials using the provided IAM role.
- Set up Terraform with version `1.5.0`.
- Initialize Terraform (`terraform init`).
- Generate and display a destroy plan (`terraform plan -destroy`).
- Destroy the Terraform-managed infrastructure (`terraform destroy -auto-approve`).

## Inputs

The workflow accepts the following input when manually triggered via `workflow_dispatch`:

action: (required)

    apply: Deploy the infrastructure.
    destroy: Remove the infrastructure.



## AWS Credentials

The workflow uses the `aws-actions/configure-aws-credentials` action to assume an IAM role. Ensure the following secrets are configured in the repository:
- `AWS_ACCOUNT_ID`: AWS account ID.
- `AWS_ROLE`: IAM role name to assume.
- `AWS_REGION`: AWS region.

## Notes
- Terraform configurations are located in the `terraform/environments/prod` directory.
- Update Terraform version or directory paths as needed for your project.
