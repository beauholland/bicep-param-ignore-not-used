Using Bicep I want to deploy resources using a superset of parameters main.parameters.json file. 

If unused parameters are present the deployment currently fails:

`InvalidTemplate - Deployment template validation failed: 'The template parameters 'paramNotUsed' in the parameters file are not valid; they are not present in the original template and can therefore not be provided at deployment time. The only supported parameters for this template are 'paramUsed'.`

**What we want**

We want to be able to use a .parameters.json file that contains a parameter that is NOT used - at least not error, or have the option to change to a warning?

One option might be adding option for tooling to: ignore, warn, error (current behaviour) if unused parameters are being passed.

**Why**

From an Azure DevOps Pipelines variables we want to be able to store variables in x2 places:
- Library Variable Sets using KeyVault for sensitive values
- .env.parameters.json files for all other non sensitive values

We have multiple .bicep files that require different parameters .env.parameters.json and don't require all params.

**Similar post here**

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

