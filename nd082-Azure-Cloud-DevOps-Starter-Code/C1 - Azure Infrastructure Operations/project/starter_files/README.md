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

deploy 
az policy definition create --name 'tagging-policy' --display-name 'deny-creation-untagged-resources' --description 'This policy ensures all indexed resources in your subscription have tags and deny deployment if they do not' --rules ./project1-tagging-policy.json  --mode All



policy 
az policy assignment create --name 'tagging-policy' --display-name 'deny-creation-untagged-resources' --policy tagging-policy


list of policy 

az policy assignment list

Open Azure portal Bash Cloud Shell then upload server.json

packer build server.json

image 

az image list

go to folder  cd project1-IaC/


variable "prefix" {
  description = "The prefix which should be used for all resources in this example"
  default = "quyetnn-project1"
}


deploy 

terraform init



terraform plan -out solution.plan

terraform show

terraform state list | while read line
do 
if [[ $line == azurerm_resource_group* ]]; then
echo $line " is a resource group and will not be deleted!"
else
echo "deleting: " $line
terraform destroy -target $line -auto-approve
fi
done

delete 

az policy assignment list
az image list
terraform plan -out solution.plan
terraform apply "solution.plan"
terraform show


### Output
az policy assignment list
az image list
terraform plan -out solution.plan
terraform apply "solution.plan"
terraform show
