# ACSFinalProject-Group30
To deploy the project infrastructure using terraform, follow below steps

#################################################################################################################################################################################

Pre-requisites:
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

#################################################################################################################################################################################
Notes:
1) We have used two branches in the Github repository which are of names "prod" and "test". It is for the best practices that we directly do not push to main(prod) branch. All the collaborators work on their local and push to test branch first and then open a pull request to marge that data in the "prod" branch after checking all the details and conflicts.
2) If we use code from any branch, we can deploy the infrastructure for all the 3 environments given in the architecture.


#################################################################################################################################################################################

Run Code:
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

1) Run the below commands to create the staging environment
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

1) Run the below commands to create the prod environment
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



#################################################################################################################################################################################

Cleanup:
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


