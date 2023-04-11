Using Bicep I want to deploy resources using a superset of parameters main.parameters.json file. 

If unused parameters are present the deployment currently fails:

`InvalidTemplate - Deployment template validation failed: 'The template parameters 'paramNotUsed' in the parameters file are not valid; they are not present in the original template and can therefore not be provided at deployment time. The only supported parameters for this template are 'paramUsed'.`

Similar post here:

[Feature Suggestion] Deployment Parameters: Allow unused paramaters in deployment

https://github.com/Azure/bicep/issues/5771

# Steps to Repro
Requires Azure CLI https://learn.microsoft.com/en-us/cli/azure/install-azure-cli

Clone Repo

In the Azure Portal > create new resource group called "param-play" or similar

Open Terminal or command prompt

Log into Azure using your credentials

`az login` automatic 

OR

`az login --use-device-code` manual 

Set your subscription - if required

az account set --subscription "YOUR SUBSCRIPTION"

az deployment group what-if --resource-group "param-play" -f "main.bicep" --parameters "main.parameters.json"

