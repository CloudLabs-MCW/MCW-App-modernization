## Exercise 2: Migrate your application with App Service Migration Assistant

Duration: 20 minutes

The first step for Parts Unlimited is to assess whether their apps have dependencies on unsupported features on Azure App Service. In this exercise, you use an **Azure Migrate** tool called the [App Service migration assistant](https://appmigration.microsoft.com/) to evaluate Parts Unlimited's web site for a migration to Azure App Service. The assessment runs readiness checks and provides potential remediation steps for common issues. Once the assessment succeeds, we will proceed with the migration as well. You will use a simulated on-premises environment hosted in virtual machines running on Azure.

### Task 1: Perform assessment for migration to Azure App Service

Parts Unlimited would like an assessment to see what potential issues they might need to address in moving their application to Azure App Service. You will use the [App Service migration assistant](https://appmigration.microsoft.com/) to assess the application and run various readiness checks.

1. In the [Azure portal](https://portal.azure.com), navigate to your **WebVM** VM by selecting **Resource groups** from Azure services list, selecting the **hands-on-lab-SUFFIX** resource group, and selecting the **WebVM** VM from the list of resources.

    ![The WebVM virtual machine is highlighted in the list of resources.](media/webvm-selection.png "WebVM Selection")

2. On the WebVM Virtual Machine's **Overview (1)** blade, copy the **Public IP address (2)**.

    ![The WebVM VM blade is displayed, Public IP Address copy button is highlighted.](media/web-vm-ip.png "WebVM Overview and Public IP")

3. Open a new browser window and navigate to the IP Address you copied.

    ![The WebVM VM blade is displayed, Public IP Address copy button is highlighted.](media/parts-umlimited-web-site.png "Parts Unlimited Web Site")

    > For testing purposes, you might want to create yourself an account on Parts Unlimited web site and purchase some products. Use the coupon code **FREE** to buy everything for free.

9. Go to Desktop of WebVM VM, open **AppServiceMigrationAssistant**.

    ![AppServiceMigrationAssistant is highlighted on the desktop.](media/appservicemigrationassistant-desktop.png "App Service Migration Assistant")

10. Once App Service Migration Assistant discovers the web sites available on the server choose **Default Web Site (1)** for migration and select **Next (2)** to start assessment.

    ![AppServiceMigrationAssistant is open. Default Web Site is selected. Next button is highlighted.](media/appservicemigration-choose-site.png "App Service Migration Assistant Web Site selection")

11. Observe the result of the assessment report. In our case, our application has successfully passed 13 tests **(1)** with no additional actions needed. Now that our assessment is complete, select **Next (2)** to proceed to the migration.

   ![Assessment report result is shown. There are 13 success metrics presented. The next button is highlighted.](media/appservicemigration-report.png "Assessment Report")

   > For the details of the readiness checks, see [App Service Migration Assistant documentation](https://github.com/Azure/App-Service-Migration-Assistant/wiki/Readiness-Checks).

### Task 2: Migrate the web application to Azure App Service

After reviewing the assessment results, you have ensured the web application is a good candidate for migration to Azure App Service. Now, we will continue the process with the migration of the application.

1. In order to continue with the migration of our web site Azure App Service Migration Assistant needs access to our Azure Subscription. Select **Copy Code & Open Browser** button to be redirected to the Azure Portal.

   ![Azure App Service Migration Assistant's Azure Login dialog is open. A device code is presented. Copy Code & Open Browser button is highlighted.](media/appservicemigration-azure-login.png "Azure Login")

2. At its first launch, you will be asked to choose a browser. Select **Microsoft Edge (1)**  and check **Always use this app (2)** checkbox. Select **OK (2)** to move to the next step.

    ![Browser choice dialog is shown. Microsoft Edge is selected. Always use this app checkbox is checked. OK button is highlighted.](media/browser-choice.png "Default Browser Selection")

3. Right-click the text box and select **Paste (1)** to paste your login code. Select **Next** to give subscription access to App Service Migration Assistant.

    ![Azure Code Login web site is open. Context menu for the code textbox is shown. Paste command from the context menu is highlighted. The next button is highlighted as a second step. ](media/appservicemigration-azure-login-code.png "Enter Authentication Code")

4. Continue the login process with your Azure Subscription credentials. When you see the message that says **You have signed in to the Azure App Service Migration Assistant application on your device** close the browser window and return to the App Service Migration Assistant.

    ![Azure Login process is complete. A message dialog is shown that indicates the login process is a success.](media/appservicemigration-azure-login-complete.png "App Service Migration Assistant authentication approval")

5. Select the Azure Migrate project we created **(1)** in the previous exercise to submit the results of our migration. Select **Next** to continue.

    ![Azure Migrate Project is set to partsunlimitedweb. The next button is highlighted.](media/appservicemigration-azure-migrate.png "Azure Migrate Hub integration")

6. In order to migrate Parts Unlimited web site, we have to create an App Service Plan. The Azure App Service Migration Assistant will take care of all the requirements needed. Select **Use existing (1)** and select the lab resource group **hands-on-lab-{DeploymentID}** as your deployment target. App Service requires a globally unique Site Name, we suggest using a pattern that matches `partsunlimited-web-{DeploymentID}` **(2)**. Select **Migrate** to start the migration process.

    ![Deployment options are presented. Existing lab resource group is selected as destination. Destination site name is set to partsunlimited-web-20X21. Migrate button is highlighted.](media/appservicemigration-migrate.png "Azure App Service Migration Assistant Options")

    > **WARNING:** If your migration fails with a **WindowsWorkersNotAllowedInLinuxResourceGroup (1)** try the migration process again, but this time selecting a different Resource Group for your deployment. If that is not possible, select a different Region.  
    >
    > ![Migration failed error screen is shown. WindowsWorkersNotAllowedInLinuxResourceGroup message is highlighted.](media/app-migration-windowsworkersnotallowed.png "Migration failed")

7. We have just completed the migration of Parts Unlimited web site from IIS on a Virtual Machine to Azure App Service. Congratulations. Let's go back to the Azure Portal and look into Azure Migrate. Search for `migrate` **(1)** on the Azure Portal and select **Azure Migrate (2)**.

    ![Azure Portal is open. The search box is filled with the migrate keyword. Azure Migrate is highlighted from the result list.](media/find-azure-migrate.png "Azure Migrate on Azure Portal Search")

8. Switch to the **Web Apps (1)** section. See the number of discovered web servers, assessed websites **(2)** and migrated websites change **(3)**. Keep in mind that you might need to wait for 5 to 10 minutes for results to show up. You can use the **Refresh** button on the page to see the latest status.

    ![Azure Migrate shows web app assessment and migration reports.](media/azure-migrate-web-app-migration-done.png "Azure Migrate Web Apps Tools")

