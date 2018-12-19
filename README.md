# ARM Template for RedCAP automated deployment


## Quick Start

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fazure-redcap-paas%2Fmaster%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

__Details__

This template automates the deployment of the RedCAP solution into Azure using managed PaaS resources. The template assumes you are deploying a version of RedCAP that supports direct connection to Azure Blob Storage. If you deploy an older version, deployment will succeed but you will need to manually provision NFS storage in Azure, and delete the new storage account. For NFS, consider:
  * https://docs.microsoft.com/en-us/azure/azure-netapp-files/
  * https://azuremarketplace.microsoft.com/en-us/marketplace/apps/softnas.softnas-cloud
  * https://azure.microsoft.com/en-us/resources/templates/nfs-ha-cluster-ubuntu/

You will need to specify a location for the deployment automation to pull your copy of the RedCAP source. This ZIP file will need to be publicly accessible via a direct URI while the deployment is running.

https://projectredcap.org/wp-content/resources/REDCapTechnicalOverview.pdf

* ARM template deploys the following:
  * Azure Web App
  * Azure DB for MySQL
  * Azure Storage Account

Review https://docs.microsoft.com/en-us/azure/mysql/concepts-pricing-tiers for details on available features, regions, and pricing models for Azure DB for MySQL.

__Setup__

This template will automatically deploy the resources necessary to run RedCAP in Azure using PaaS (Platform as a Service) features. After the template is deployed, deployment automation will download the RedCAP ZIP file you specify, and install it in your web app. It will then automatically update the database connection information in the app. It will then update a few settings in the database, and configure Azure file storage if you have that version of RedCAP. It will also create the initial storage container.

If you need to connect to the MySQL database using the MySQL client, you will need to open the firewall to your managed MySQL instance and allow connections from the location where you will run the client. Here are the instructions:
https://docs.microsoft.com/en-us/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal#configure-a-server-level-firewall-rule

(Add your current IP address by clicking "+ Add My IP")

Once you've opened the firewall, you will need your database name. The credentials are those you supplied in this template. The name is available from the portal where you updated the firewall rules:

  ![alt text][MySql]

Please also review:
https://docs.microsoft.com/en-us/azure/mysql/concepts-ssl-connection-security

### Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.


[MySql]: ./images/mysql.png