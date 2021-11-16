# Exercise 1: Setting up Azure Migrate

Duration: 10 minutes

Azure Migrate provides a centralized hub to assess and migrate on-premises servers, infrastructure, applications, and data to Azure . It provides a single portal to start, run, and track your migration to Azure. Azure Migrate comes with a range of tools for assessment and migration that we will use during our lab. We will use Azure Migrate as the central location for our assessment and migration efforts.

1. Default Browser - Make sure Edge is the default browser by navigating to Start>Settings>Default Apps as shown below

   ![Find Default Apps](media/DefaultApps.png "Find Default Apps")

   ![Edge as default browser](media/Edge-DefaultBrowser.png "Set Edge as Default Browser")

1. Open the **Azure portal** from the shortcut and log in to Azure. When prompted, use the below credentials to complete the login process.

    * Email/Username: <inject key="AzureAdUserEmail"></inject>
    * Password: <inject key="AzureAdUserPassword"></inject>


    ![Azure Portal shorcut](https://raw.githubusercontent.com/ShivaUdari/MCW-App-modernization/stage/Hands-on%20lab/media/azure-portal-start.png "Azure Portal shortcut")

1. Select your **resource group**. 

    ![Select your resource group.](media/resource-group-1.png "Resource Group")

1. Select **Create** inside the resource group to add a new resource.

    ![Lab resource group is open. Resource Add button is highlighted.](media/portal-add-resource-1.png "Lab Resource Group")

1. Type **Azure Migrate** into the search box and select **Azure Migrate** from the dropdown.

    ![Azure Portal new resource page is open. Search box is filled with Azure Migrate.](media/azure-migrate-search.png "Marketplace Search for Azure Migrate")

1. Select **Create** to continue.

    ![Azure Migrate resource creation screen is open. Create button is highlighted.](media/azure-migrate-create.png "Creating Azure Migrate")

1. As part of our migration project for Parts Unlimited, we will first assess and migrate their Web Application living on IIS, on a VM. Select **Web Apps** to continue.

    ![Azure Migrate is open. Web Apps section is highlighted.](media/azure-migrate-web-app-1.png "Azure Migrate Web Apps")

1. Select **Create project**.

    ![Azure Migrate is open. Web Apps section is selected. Create project button is highlighted.](media/azure-migrate-web-app-2.png "Azure Migrate Create project")

1. Type **partsunlimitedweb<inject key="DeploymentID" enableCopy="false"/>**  as your project name. Select **Create** to continue. 

    ![Azure Migrate project settings page is shown. Project name is set to partsunlimitedweb. Create button is highlighted.](media/azure-migrate-create-project-settings.png "Azure Migrate Project Creation")

1. Once your project is created **Azure Migrate** will show you default **Web App Assessment (1)** and **Web App Migration (2)** tools (You might need to refresh your browser). For Parts Unlimited web site, **App Service Migration Assistant** is the one we have to use. Download links are presented in Azure Migrate's Web Apps page. In our case, our lab environment comes with App Service Migration Assistant pre-installed on Parts Unlimited's web server.

    ![Azure Migrate Web App assessment and migration tools are presented.](media/azure-migrate-web-app-3.png "Azure Migrate Web Apps Capabilities")

1. Another aspect of our migration project will be the database for Parts Unlimited's web site. We will have to assess the database's compatibility and migrate to Azure SQL Database. Let's switch to the **Databases (only) (1)** section in Azure Migrate. Select **Click here (2)** hyperlink for Assessment tools.

    ![Azure Migrate is open. Databases section is selected. Click here link for assessment tools is highlighted.](media/azure-migrate-web-app-4.png "Azure Migrate Databases")

1. We will use **Azure Migrate: Database Assessment** to assess Parts Unlimited's database hosted on a SQL Server 2008 R2 server. Pick **Azure Migrate: Database Assessment (1)** and select **Add tool (2)**.

    ![Azure Migrate Database Assessment option is selected for Azure Migrate tools. Add tool button is highlighted.](media/azure-migrate-database-assessment-tool.png "Azure Migrate Database Assessment Tools")

1. Now, we can see a download link for the **Data Migration Assessment (1)** tool under assessment tools in Azure Migrate. In our case, our lab environment comes with the Data Migration Assessment pre-installed on Parts Unlimited's database server. Select **Click here (2)** under the **Migration Tools** section to continue.

    ![Data Migration Assessment tool's download link is shown. Click here link for migration tools is highlighted.](media/azure-migrate-web-app-5.png "Azure Migrate DMA Download")

1. We will use **Azure Migrate: Database Migration** to migrate Parts Unlimited's database to an Azure SQL Database. Pick **Azure Migrate: Database Assessment (1)** and select **Add tool (2)**.

    ![Azure Migrate Database Migration option is selected for Azure Migrate tools. Add tool button is highlighted.](media/azure-migrate-database-migration-tool.png "Azure Migrate Database Migration Tool")

1. Now we have all the assessment and migration tools/services we need for Parts Unlimited ready to go under the Azure Migrate umbrella.

    ![Azure Migrate databases section is open. Azure Migrate Database Assessment and Database Migration tools are presented.](media/azure-migrate-web-app-6.png "Azure Migrate Database Migration and Assessment Tools")
