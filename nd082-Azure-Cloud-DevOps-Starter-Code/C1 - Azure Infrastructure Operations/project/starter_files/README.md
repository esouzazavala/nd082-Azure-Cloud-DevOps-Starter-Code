# Azure Infrastructure Operations Project: Deploying a scalable IaaS web server in Azure

### Introduction
For this project, you will write a Packer template and a Terraform template to deploy a customizable, scalable web server in Azure.

### Getting Started
1. Clone this repository

2. Create your infrastructure as code

3. Update this README to reflect how someone would use your code.

### Dependencies
1. Create an [Azure Account](https://portal.azure.com) 
2. Install the [Azure command line interface](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
3. Install [Packer](https://www.packer.io/downloads)
4. Install [Terraform](https://www.terraform.io/downloads.html)

### Instructions

2.1. ✔️ Navigate to your repository

2.2. ✔️ Authenticate to Azure the open Azure portal Bash Cloud Shell to upload project1-tagging-policy.json

2.3. ✔️ Deploy a policy

Create the Policy Definition:

az policy definition create --name 'tagging-policy' --display-name 'deny-creation-untagged-resources' --description 'This policy ensures all indexed resources in your subscription have tags and deny deployment if they do not' --rules ./project1-tagging-policy.json  --mode All


2.4. ✔️ Create the Policy Assignment

az policy assignment create --name 'tagging-policy' --display-name 'deny-creation-untagged-resources' --policy tagging-policy


2.5. ✔️ List the policy assignments to verify
az policy assignment list

<img width="1554" height="685" alt="image" src="https://github.com/user-attachments/assets/7b364310-88a5-4bd8-baef-9d6a1f4289a5" />




2.6. ✔️ Create a Server Image with Packer
✔️ Open Azure portal Bash Cloud Shell then upload server.json

✔️ Create a Server Image using below packer command

packer build server.json

<img width="1533" height="668" alt="image" src="https://github.com/user-attachments/assets/356adfd1-05a5-4355-9ac7-113efcb8c6d2" />

✔️ View Images

az image list
<img width="1542" height="596" alt="image" src="https://github.com/user-attachments/assets/c803756d-19c0-4f8f-8755-450107f2506d" />


2.7. ✔️ Create the infrastructure with Terraform Template

Go to folder cd project1-IaC/

Our Terraform template will allow us to reliably create, update, and destroy our infrastructure

Customize vars.tf

Variables from vars.tf are called from mains.tf, for example the variable prefix is called as:

${var.prefix}

In vars.tf, the description and value is assigned in the following manner:

variable "prefix" {
  description = "The prefix which should be used for all resources in this example"
  default = "quyetnn-project1"
}
See all variable in vars.tf


2.8. ✔️ Deploy infrastructure

Initializing Working Directories

terraform init

Create infrastructure plan

terraform plan -out solution.plan


Deploy the infrastructure plan

terraform apply "solution.plan"



View infrastructure

terraform show

<img width="1547" height="711" alt="image" src="https://github.com/user-attachments/assets/e6be1298-5e7f-4b71-9a82-2e936c9a317c" />


<img width="1167" height="738" alt="image" src="https://github.com/user-attachments/assets/9b6faddd-5908-46fb-9535-c220eddcdeb2" />

Terraform template  

Check-out the vars.tf file!

There you may need to fill-out with the right values:

initailize terraform 

terraform init

review the solution to deploy

terraform pan 

solution.plan 

terraform plan -out solution.plan 

build a dn deplot the solution 

terraform apply solution.plan

terraform show 

<img width="1010" height="541" alt="image" src="https://github.com/user-attachments/assets/aad0aa2e-b4e8-448a-9554-648a5b79e420" />


<img width="1782" height="179" alt="image" src="https://github.com/user-attachments/assets/3a7638d9-0bc7-4437-af2a-53adcf2aa5bf" />

<img width="1852" height="240" alt="image" src="https://github.com/user-attachments/assets/c3b3a7b0-411b-4493-8f44-9ee18c82d85f" />

<img width="1220" height="204" alt="image" src="https://github.com/user-attachments/assets/f6fb077c-8f77-4cec-8eed-149730cf7031" />

<img width="1855" height="545" alt="image" src="https://github.com/user-attachments/assets/aa26a3b3-54d0-4419-b0e6-55246016d876" />


destoy 

terraform destory 

 


Destroy infrastructure (when completed) using clean_resources.sh to delete all resources except Azuredevops resource group
terraform state list | while read line

do 
if [[ $line == azurerm_resource_group* ]]; then
echo $line " is a resource group and will not be deleted!"
else
echo "deleting: " $line
terraform destroy -target $line -auto-approve
fi
done

terraform state list | while read line
do 
if [[ $line == azurerm_resource_group* ]]; then
echo $line " is a resource group and will not be deleted!"
else
echo "deleting: " $line
terraform destroy -target $line -auto-approve
fi
done
<img width="623" height="216" alt="image" src="https://github.com/user-attachments/assets/c52c57f7-a11f-4f4c-adf8-7f03e9bdb52a" />


Using terraform state list command to skip destroying azurerm_resource_group which lab user can not delete it.





Delete images
az image delete -g Azuredevops -n MyPackerImage
