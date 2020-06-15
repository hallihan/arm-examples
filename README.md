# Parameterized Azure ARM Template Deployment

This sample template will deploy multiple tiers of resources into an Azure Resource Group.  Each tier has configurable elements, to show how you can expose parameterization to the end user.

![Azure Public Test Date](https://azurequickstartsservice.blob.core.windows.net/badges/101-parameterized-template-example/PublicLastTestDate.svg)
![Azure Public Test Result](https://azurequickstartsservice.blob.core.windows.net/badges/101-parameterized-template-example/PublicDeployment.svg)

![Azure US Gov Last Test Date](https://azurequickstartsservice.blob.core.windows.net/badges/101-parameterized-template-example/FairfaxLastTestDate.svg)
![Azure US Gov Last Test Result](https://azurequickstartsservice.blob.core.windows.net/badges/101-parameterized-template-example/FairfaxDeployment.svg)

![Best Practice Check](https://azurequickstartsservice.blob.core.windows.net/badges/101-parameterized-template-example/BestPracticeResult.svg)
![Cred Scan Check](https://azurequickstartsservice.blob.core.windows.net/badges/101-parameterized-template-example/CredScanResult.svg)

## Deploy this template to Azure
[![Deploy To Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhallihan%2Farm-examples%2Fmain%2Fazuredeploy.json)
[![Deploy To Azure US Gov](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazuregov.svg?sanitize=true)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhallihan%2Farm-examples%2Fmain%2Fazuredeploy.json)
[![Visualize](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.svg?sanitize=true)](http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fhallihan%2Farm-examples%2Fmain%2Fazuredeploy.json)

*Note: If you fork this repository, you will need to modify the link in [README.md](README.md) to point to your repo.  If you create a separate branch for testing, you will have to include a change to this link to point to your branch as well. You must include a URL-encoded link to the [azuredeploy.json](azuredeploy.json) file after /uri/ in the link defined for the deployment button. If you use the link in [DEPLOY.html (hosted with Github Pages or any Static Web Location)](https://hallihan.github.io/arm-examples/DEPLOY.html) the template URI will be constructed automatically.* 

## Overview

### Front End
There are three user accessible front-ends for the deployment:
* An Azure Bastion Service deployed into the VNET to allow ssh access to VMs that do not have public IP addresses.
* An Azure App Gateway that will load balance HTTP requests on port 80 to the back-end tier nodes.
* An Azure VM "Jump box" that allows ssh access, and which also has a custom startup script that uses the private ip addresses gathered from the back-end.

All 3 front-ends are protected by Network Security Groups and only allow access from an IP address or CIDR provided in the deployment parameters.

### Middle Tier
The middle-tier currently serves no real purpose other than to demonstrate variable configuration deployment of 0, 1, or 3 VMs as is seen in services that include a high-availability configuration when deployed.

### Back End
Each node in the back-end tier currently runs a script to start a simple web server on port 80 (See [ExamplePostInstall2.sh](scripts/ExamplePostInstall2.sh)).  The web server will display a static html file that includes the virtual machine name retrieved from the [Azure Instance Metadata Service](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/instance-metadata-service).

## Topics Covered:

#### [Naming Parameters to be User Friendly](detail/UserFriendlyParameters.md)
#### [Using Variables to Centralize Configurable Elements](detail/ComplexVariables.md)
#### [Use Deployment Properties to avoid hardcoded URIs](detail/TemplateLink.md)
#### [Use Linked Template for Multiple Resources (IaaS)](detail/VMTemplate.md) *TODO*
#### [Use Linked Template to Limit Main Template Complexity (App Gateway)](detail/AGTemplate.md) *TODO*

## [See License](LICENSE)

`Tags: ARM, Variables, Linked Templates, IaaS`