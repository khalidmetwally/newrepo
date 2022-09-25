#  AWS ECS/Fargate implementation with Terraform and Terragrunt

-----------------------
#### It creates the following resources:

	1- VPC
	2- 2 public and 2 private subnets
	3- Internet GW for public subnets
	4- 2 Nat GWs for private subnets
	5- 2 Elastic IP's for Nat GWs
	6- 2 Security Groups: for ALB and Tasks
	7- ALB + Target Group
	8- ECR for docker images
	9- ECS fargate + Service + Taskdefinition

-----------------------

#### How it works:
	1- add your own values in `terraform.tfvars` # I've added my own for example
	2- setup your AWS creds. 
	3- execute: `terragrunt init` , accept creating Backend S3 bucket if not exist.
	4- execute: `terragrunt plan`
	5- execute: `terragrunt apply` 
	
-----------------------


#### Input values for `terraform.tfvars` example:
-----------------------

name                = "the name of the stack" eg: "plana-ecs-vpc"

environment         = "the name of the environment" eg: "case"

availability_zones  = ""a comma-separated list of availability zones" eg:["us-east-1a", "us-east-1b"]

cidr                = "The CIDR block for the VPC." eg:"10.0.0.0/16"

private_subnets     = "a list of CIDRs for private subnets" eg:["10.0.0.0/24", "10.0.1.0/24"]

public_subnets      = "a list of CIDRs for public subnets" eg:["10.0.100.0/24", "10.0.101.0/24"]

tls_certificate_arn = "The ARN of the certificate that the ALB uses for https" eg:"arn:aws:acm:us-east-1:123456789:certificate/12345-6789"

container_image     = "Docker image to be launched" eg:"nginxdemos/hello" # It's better to use this one than the standard "nginx" image to show loadbalancing

container_memory    = "The amount of memory used by the task" eg:512

health_check_path   = "Http path for task health check"  eg:"/"

-----------------------
