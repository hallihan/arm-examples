# Sample Parameterized Azure ARM Deployment

This sample template will deploy multiple tiers of resources into an Azure Resource Group.  Each tier has configurable elements, to show how you can expose parameterization to the end user.

## Overview

### Front End
There are three user accessible front-ends for the deployment:
* An Azure Bastion Service deployed into the VNET to allow ssh access to VMs that do not have public IP addresses.
* An Azure App Gateway that will load balance HTTP requests on port 80 to the back-end tier nodes.
* An Azure VM "Jump box" that allows ssh access, and which also has a custom startup script that uses the private ip addresses gathered from the back-end.

All 3 front-ends are protected by Network Security Groups and only allow access from an IP address or CIDR provided in the deployment parameters.

### Middle Tier
The middle-tier currently serves no real purpose other than to demonstrate fixed configuration deployment of 0, 1, or 3 VMs, as is seen in services that include a high-availability configuration when deployed.

### Back End
Each node in the back-end tier currently runs a script to start a simple web server on port 80 (See ExamplePostInstall2.sh).  The web server will display a static html file that includes the virtual machine name that has been retrieve from the [Azure Instance Metadata Service](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/instance-metadata-service).

## Deploy this template to Azure
[![Deploy to Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true "Deploy to Azure Button")](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhallihan%2Farm-examples%2Fmain%2Fazuredeploy.json)

*Note: If you fork this repository, you will need to modify the link in [README.md#4](README.md#4) to point to your repo.  If you create a separate branch for testing, you will have to include a change to this link to point to your branch as well. You must include a URL-encoded link to the raw base deployment json file after /uri/ in the link defined for the deployment button.*

## Topics Covered:

#### [Naming Parameters to be User Friendly](UserFriendlyParameters.md) *TODO*
#### [Using Variables to Centralize Configurable Elements](ComplexVariables.md) *TODO*
#### [Use Linked Template for Multiple Resources (IaaS)](VMTemplate.md) *TODO*
#### [Use Linked Template to Limit Main Template Complexity (App Gateway)](AGTemplate.md) *TODO*

## [See License](LICENSE)