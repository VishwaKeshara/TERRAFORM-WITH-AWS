# TerraformAC

This repository contains a Terraform project that provisions a simple AWS application network with two EC2 web server instances behind an Application Load Balancer.

## What this project creates

- AWS VPC with CIDR `10.0.0.0/16`
- Two public subnets in `us-east-1a` and `us-east-1b`
- Internet Gateway and route table for public internet access
- Security Group allowing HTTP (80) and SSH (22) from anywhere
- S3 bucket named `vishwaterraform2026project`
- Two EC2 instances using `ami-0f8a61b66d1accaee` and `t2.micro`
- User data scripts to install Apache and serve a simple HTML page
- Application Load Balancer with target group and listener forwarding traffic to both EC2 instances

## Files

- `main.tf` - Main Terraform resources
- `provider.tf` - AWS provider configuration
- `variables.tf` - Terraform variables
- `userdata.sh` - Initialization script for webserver1
- `userdata1.sh` - Initialization script for webserver2
- `terraform.tfstate` / `terraform.tfstate.backup` - Terraform state files

## Requirements

- Terraform installed
- AWS CLI configured with credentials that have permissions to create VPC, subnet, EC2, security group, S3 bucket, and load balancer resources

## Usage

1. Initialize Terraform

```bash
terraform init
```

2. Review the execution plan

```bash
terraform plan
```

3. Apply the configuration

```bash
terraform apply -auto-approve
```

4. After apply completes, note the ALB DNS name output:

```bash
terraform output alb_dns_name
```

Open the ALB DNS name in a browser to view the deployed web page.

## Notes

- The project hardcodes the AWS region as `us-east-1` in `provider.tf`.
- The SSH port is open to the internet due to the security group configuration; restrict this in production.
- The web pages on each instance differ slightly in text to identify the instance.
- The S3 bucket is created but not currently used by the deployed user data script.

## Cleanup

To destroy the resources created by this project:

```bash
terraform destroy -auto-approve
```

