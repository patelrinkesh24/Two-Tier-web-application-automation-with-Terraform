# Two-Tier Web Application Automation with Terraform

## About the Project

This project is a part of the ACS730 course, aimed at demonstrating the application of deployment automation, configuration management, and source control tools to create a scalable two-tier web application hosting solution using Terraform. The solution is designed to support DevOps practices, ensure security compliance, and optimize cloud infrastructure management.

## Project Overview

The project involves deploying a static web application on an AWS environment, utilizing Auto Scaling Groups (ASG) for scalability and load balancers for traffic management. The infrastructure is managed using Terraform, ensuring a modular, consistent, and repeatable deployment process. Security is a key focus, with automated security scans integrated into the CI/CD pipeline.
## 1. Architecure
![architecture](https://github.com/user-attachments/assets/98f83e75-aaaa-46a8-99e1-e02144bf2188)

## 2. Traffic Flow
![two-tier automation](https://github.com/user-attachments/assets/ba8de907-4ec2-40f4-9729-2b7bb7d6531a)


## Key Features

- **Scalable Architecture**: The application is deployed across multiple availability zones, with auto-scaling based on CPU load.
- **Infrastructure as Code**: The entire infrastructure is defined using Terraform, allowing for consistent and reliable deployments.
- **Security Automation**: The project includes automated security scans using GitHub Actions, ensuring the Terraform code adheres to security standards.
- **Environment-Specific Configuration**: Separate environments (Dev, Staging, Prod) with distinct configurations, including VPC CIDR ranges and instance types.

## Benefits of DevOps Practices

- **Increased Deployment Speed**: Automation reduces manual intervention, speeding up deployment processes.
- **Improved Collaboration**: Source control and CI/CD pipelines enhance team collaboration and code quality.
- **Enhanced Security**: Automated security scans and compliance checks ensure the infrastructure is secure from the ground up.
- **Scalability and Reliability**: The use of auto-scaling groups and load balancers ensures the application can handle varying traffic loads efficiently.

## Core Infrastructure Design

- **Auto Scaling Groups (ASG)**: Configured to maintain a minimum of 1 and a maximum of 4 instances, scaling based on CPU usage.
- **Load Balancers**: Distribute traffic across instances, ensuring high availability.
- **VPC and Subnets**: Each environment (Dev, Staging, Prod) has its own VPC and subnets, with identical subnet sizes.
- **S3 Buckets**: Used to store Terraform state files and web application images.

## Security Considerations

- **IAM Roles**: Implemented to restrict access to AWS resources.
- **Security Groups**: Configured to control inbound and outbound traffic to EC2 instances.
- **GitHub Actions**: Integrated to perform static code analysis and security validation on every code push.

## Deployment Instructions

### Pre-requisites:
1) Clone the code from the Github repository (https://github.com/rajat9093/ACSFinalProject-Group30.git) into your Cloud9 environment

2) Create 3 ssh keys for the EC2 instances in different environments with the below commands (if you change the name, it need to be updated in the code also),
	ssh-keygen -t rsa -f ~/.ssh/group30-dev
	ssh-keygen -t rsa -f ~/.ssh/group30-staging
	ssh-keygen -t rsa -f ~/.ssh/group30-prod

3) Create 3 S3 buckets in your AWS account with the below names for the different environments. (Keep the same names as below or the names needs to be updated in the config.tf files and main.tf file also)
	group30-bucket-dev
	group30-bucket-staging
	group30-bucket-prod

4) Create new bucket "images-bucket-group30" for the images purpose to show it on the webserver. Upload images to the S3 bucket and change the images name to the "install_httpd.sh.tpl" file in the path "~/environment/ACSFinalProject-Group30/modules/aws_webservers"

5) Provide your AWS Cloud9 instance Public & Private IP address in the "variable.tf" file in webservers of different environments. This is to ensure that we can login to our bastion host in AWS and do our work further.

### Notes:
1) We have used two branches in the Github repository which are of names "prod" and "test". It is for the best practices that we directly do not push to main(prod) branch. All the collaborators work on their local and push to test branch first and then open a pull request to marge that data in the "prod" branch after checking all the details and conflicts.
2) If we use code from any branch, we can deploy the infrastructure for all the 3 environments given in the architecture.

### Run Code:
1) Run the below commands to create the dev environment
	Network module,
	cd ~/environment/ACSFinalProject-Group30/terraform/network/dev-network
	terraform init
	terraform plan
	terraform apply --auto-approve

	Webserver module,
	cd ~/environment/ACSFinalProject-Group30/terraform/webservers/dev-webserver
	terraform init
	terraform plan
	terraform apply --auto-approve

2) Run the below commands to create the staging environment
	Network module,
	cd ~/environment/ACSFinalProject-Group30/terraform/network/staging-network
	terraform init
	terraform plan
	terraform apply --auto-approve

	Webserver module,
	cd ~/environment/ACSFinalProject-Group30/terraform/webservers/staging-webserver
	terraform init
	terraform plan
	terraform apply --auto-approve

3) Run the below commands to create the prod environment
	Network module,
	cd ~/environment/ACSFinalProject-Group30/terraform/network/prod-network
	terraform init
	terraform plan
	terraform apply --auto-approve

	Webserver module,
	cd ~/environment/ACSFinalProject-Group30/terraform/webservers/prod-webserver
	terraform init
	terraform plan
	terraform apply --auto-approve

### Cleanup:
1) It is necessary to delete all the resources as it will cost us. We can follow below commands to delete the resources in the idle sequence.
Commands:

	cd ~/environment/ACSFinalProject-Group30/terraform/webservers/dev-webserver
	terraform destroy --auto-approve

	cd ~/environment/ACSFinalProject-Group30/terraform/network/dev-network
	terraform destroy --auto-approve

	cd ~/environment/ACSFinalProject-Group30/terraform/webservers/staging-webserver
	terraform destroy --auto-approve

	cd ~/environment/ACSFinalProject-Group30/terraform/network/staging-network
	terraform destroy --auto-approve

	cd ~/environment/ACSFinalProject-Group30/terraform/webservers/prod-webserver
	terraform destroy --auto-approve

	cd ~/environment/ACSFinalProject-Group30/terraform/network/prod-network
	terraform destroy --auto-approve

## Conclusion

This project highlights the importance of automation, security, and scalability in modern cloud deployments. The challenges faced during the project included configuring auto-scaling policies and integrating security scans into the CI/CD pipeline. The experience gained has deepened my understanding of DevOps practices and Infrastructure as Code.
