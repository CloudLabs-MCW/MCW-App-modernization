## Exercise 1: Setting up Azure Migrate

Duration: 10 minutes

Azure Migrate provides a centralized hub to assess and migrate on-premises servers, infrastructure, applications, and data to Azure . It provides a single portal to start, run, and track your migration to Azure. Azure Migrate comes with a range of tools for assessment and migration that we will use during our lab. We will use Azure Migrate as the central location for our assessment and migration efforts.

1. In the WEB-VM provided to you left side of screen go to Desktop and open Microsoft Edge browser. Browse https://portal.azure.com, navigate to your lab resource group **hands-on-lab-{DeploymentID}**. Select **Add** to add a new resource.

>Note: You can get your DeploymentID in environments tab of lab guide. Make a note of this ID, it will be used in throughout of this lab

    ![Lab resource group is open. Resource Add button is highlighted.](media/portal-add-resource.png "Lab Resource Group")

2. Type **Azure Migrate** into the search box and hit **Enter** to start the search.

    ![Azure Portal new resource page is open. Search box is filled with Azure Migrate.](media/azure-migrate-search.png "Marketplace Search for Azure Migrate")

3. Select **Create** to continue.

    ![Azure Migrate resource creation screen is open. Create button is highlighted.](media/azure-migrate-create.png "Creating Azure Migrate")

4. As part of our migration project for Parts Unlimited, we will first assess and migrate their Web Application living on IIS, on a VM. Select **Web Apps** to continue.

    ![Azure Migrate is open. Web Apps section is highlighted.](media/azure-migrate-web-apps.png "Azure Migrate Web Apps")

5. Select **Create project**.

    ![Azure Migrate is open. Web Apps section is selected. Create project button is highlighted.](media/azure-migrate-create-project.png "Azure Migrate Create project")

6. Type **partsunlimitedweb** as your project name. Select **Create** to continue.

    ![Azure Migrate project settings page is shown. Project name is set to partsunlimitedweb. Create button is highlighted.](media/azure-migrate-create-project-settings.png "Azure Migrate Project Creation")

7. Once your project is created **Azure Migrate** will show you default **Web App Assessment (1)** and **Web App Migration (2)** tools (You might need to refresh your browser). For Parts Unlimited web site, **App Service Migration Assistant** is the one we have to use. Download links are presented in Azure Migrate's Web Apps page. In our case, our lab environment comes with App Service Migration Assistant pre-installed on Parts Unlimited's web server.

    ![Azure Migrate Web App assessment and migration tools are presented.](media/azure-migrate-web-app-migration.png "Azure Migrate Web Apps Capabilities")

8. Another aspect of our migration project will be the database for Parts Unlimited's web site. We will have to assess the database's compatibility and migrate to Azure SQL Database. Let's switch to the **Databases (1)** section in Azure Migrate. Select **Click here (2)** hyperlink for Assessment tools.

    ![Azure Migrate is open. Databases section is selected. Click here link for assessment tools is highlighted.](media/azure-migrate-database-assessment.png "Azure Migrate Databases")

9. We will use **Azure Migrate: Database Assessment** to assess Parts Unlimited's database hosted on a SQL Server 2008 R2 server. Pick **Azure Migrate: Database Assessment (1)** and select **Add tool (2)**.

    ![Azure Migrate Database Assessment option is selected for Azure Migrate tools. Add tool button is highlighted.](media/azure-migrate-database-assessment-tool.png "Azure Migrate Database Assessment Tools")

10. Now, we can see a download link for the **Data Migration Assessment (1)** tool under assessment tools in Azure Migrate. In our case, our lab environment comes with the Data Migration Assessment pre-installed on Parts Unlimited's database server. Select **Click here (2)** under the **Migration Tools** section to continue.

    ![Data Migration Assessment tool's download link is shown. Click here link for migration tools is highlighted.](media/azure-migrate-database-migration.png "Azure Migrate DMA Download")

11. We will use **Azure Migrate: Database Migration** to migrate Parts Unlimited's database to an Azure SQL Database. Pick **Azure Migrate: Database Assessment (1)** and select **Add tool (2)**.

    ![Azure Migrate Database Migration option is selected for Azure Migrate tools. Add tool button is highlighted.](media/azure-migrate-database-migration-tool.png "Azure Migrate Database Migration Tool")

12. Now we have all the assessment and migration tools/services we need for Parts Unlimited ready to go under the Azure Migrate umbrella.

    ![Azure Migrate databases section is open. Azure Migrate Database Assessment and Database Migration tools are presented.](media/azure-migrate-database-migration-ready.png "Azure Migrate Database Migration and Assessment Tools")

