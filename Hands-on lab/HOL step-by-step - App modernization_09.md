# Exercise 5: Using serverless Azure Functions to process orders

Duration: 30 minutes

With its migration to Azure, Parts Unlimited plans to launch a series of campaigns to increase its sales. Their current architecture is processing purchase orders synchronously and is coupled with their front end. Parts Unlimited is looking for ways to decouple its order processing system and make sure it can scale independently from the web front end when orders increase.

You suggest a serverless approach that can handle order processing and the creation of invoices for processed orders. In this exercise, you will deploy a serverless Azure Function that will listen to an Azure Storage Queue and process orders as they come. Parts Unlimited has already implemented the changes required to push the jobs into a queue of your choice.

## Task 1: Deploying Azure Functions


1. Select the Start menu and search for **Visual Studio Code**. Select **Visual Studio Code** to run it.

    ![Start Menu is open. Visual Studio Code is typed in the search box. Visual Studio Code is highlighted from the list of search results.](media/vscode-start-menu.png "Visual Studio Code")

1. Open the **File (1)** menu and select **Open Folder... (2)**.

    ![File menu is open in Visual Studio Code. Open Folder... command is highlighted.](media/vscode-open-folder.png "Open Folder")

1. Navigate to `C:\MCW\MCW-App-modernization-stage\Hands-on lab\lab-files\src-invoicing-functions\FunctionApp` and select **Select Folder**.

1. Select **Install** to install extensions required for your Azure Functions project. This will install C# for Visual Studio Code and Azure Functions Extension for Visual Studio Code.

    ![Visual Studio Code is on screen. Install extensions button is highlighted.](media/vscode-extenstions-install.png "Extension Install")

1. Once install is **Finished (1)** select **Restore (2)** to download dependencies for the project.

    ![Visual Studio Code is on screen. Restore dependencies button is highlighted.](media/vscode-restore-dependencies.png ".NET Restore")
    
        - If the C# extension is aready present in VS code, it may not ask you to restore.

1. When restore is complete close the tabs titled **Extension (1) (2)** and the **welcome tab (3)**. Select **Azure (4)** from the left menu and select **Sign into Azure (5)**. Select **Edge** as your browser if requested.

    ![Clouse buttons for all tabs are highlighted. Azure button from the left bar is selected. Sign in to Azure link is highlighted.](media/vscode-azure-signin.png "VSCode Azure Sign In")

1. Enter your Azure credentials and Sign In.

1. Close the browser tab and minimize the browser window once your sign in is complete.

1. Within the Visual Studio Code window, drill down **(1)** the resource in your subscription. Right click on your Azure Function named **parts-func-{uniquesuffix} (2)** and select **Deploy to Azure Function App... (3)**.

    ![Azure subscription is shown. The function app **parts-func-{uniquesuffix} (2)** is selected. On the context menu Deploy to Function App is highlighted.](media/vscode-deploy-function-app.png "Deploy to Function App")

1. Select **Deploy**.

    ![VS Code deployment approval dialog is open.](media/vscode-deploy-approval.png "Deploy overwrite")

## Task 2: Connecting Function App and App Service

1. In the [Azure portal](https://portal.azure.com), navigate to your `parts` Storage Account resource by selecting **Resource groups** from Azure services list, selecting the **hands-on-lab-SUFFIX** resource group, and selecting the `parts{uniquesuffix}` Storage Account from the list of resources.

    ![The parts{uniquesuffix} Storage Account is highlighted in the list of resources in the hands-on-lab-SUFFIX resource group.](media/select-storage-account.png "Storage Resource Selection")

1. Switch to the **Access keys (1)** blade, and select **Show keys (2)**. Select the copy button for the first connection string **(3)**. Paste the value into a text editor, such as Notepad.exe, for later reference.

    ![Access keys blade is open. Show keys button is highlighted. The copy button for the first connection string is pointed.](media/storage-account-connection-copy.png "Storage Access Keys")

1. Go back to the resource list and navigate to your `partsunlimited-web-{uniquesuffix}` **(2)** App Service resource. You can search for `partsunlimited-web` **(1)** to find your Web App and App Service Plan

   ![The search box for the resource is filled in with partsunlimited-web. The partsunlimited-web-20 Azure App Service is highlighted in the list of resources in the hands-on-lab-SUFFIX resource group.](media/resource-group-appservice-resource.png "Resources")

1. Switch to the **Configuration (1)** blade, and select **+New connection string (2)**.

    ![App service configuration panel is open. +New connection string button is highlighted.](media/app-service-settings-new-connection.png "App Service Configuration")

1. On the **Add/Edit connection string** panel, enter the following:

   - **Name(1)**: Enter `StorageConnectionString`.
   - **Value**: Enter Storage Connection String you copied in Step 2.
   - **Type (3)**: Select **Custom**
   - **Deployment slot setting (4)**: Check this option to make sure connection strings stick to a deployment slot. This will make sure you can have different settings for staging and production.

    ![Add/Edit Connection string panel is open. The name field is set to StorageConnectionString. The value field is set to the connection string copied in a previous step. Type is set to Custom. The deployment slot setting checkbox is checked. OK button is highlighted. ](media/app-service-storage-connection.png "Deployment Slot Configuration")

1. Select **OK (5)**.

1. Select **Save** and **Continue** for the following confirmation dialog.

    ![App Service Configuration page is open. Save button is highlighted.](media/app-service-settings-save.png "App Service Configuration")

1. Go back to the resource list and navigate to your `parts-func-{uniquesuffix}` **(2)** Function App resource. You can search for `func` **(1)** to find your function app.

   ![The search box for the resource is filled in with func. The parts-func-{uniquesuffix} Function App is highlighted in the list of resources in the hands-on-lab-SUFFIX resource group.](media/select-function-app.png "Function App Resource Selection")

1. Switch to the **Configuration (1)** blade, and select **+New application setting (2)**.

    ![Function App configuration panel is open. +New application setting button is highlighted.](media/function-app-app-settings-new.png "Function App Configuration")

1. On the **Add/Edit connection string** panel, enter the following:

    - **Name(1)**: Enter `DefaultConnection`.
    - **Value**: Enter SQL Connection String you copied in Exercise 3, Task 5, Step 3.

    ![Add/Edit Connection string panel is open. The name field is set to StorageConnectionString. The value field is set to the connection string copied in a previous step. Type is set to Custom. The deployment slot setting checkbox is checked. OK button is highlighted.](media/function-app-sql-setting.png "Function App Configuration")

1. Select **OK (3)**.

1. Select **Save** and **Continue** for the following confirmation dialog.

    ![Function App Configuration page is open. Save button is highlighted.](media/function-app-setting-save.png "Function App Configuration")

## Task 3: Testing serverless order processing

In this task, we will submit a new order on the Parts Unlimited website and observe the order's processing on the order details page. Once the order is submitted, the web front-end will put a job into an Azure Storage Queue. The Function App that we previously deployed is set to listen to the queue and pull jobs for processing. Once order processing is done, a PDF file will be created, and the link for the PDF file will be accessible on the order details page.

1. Go back to the resource list and navigate to your `partsunlimited-web-{uniquesuffix}` **(2)** App Service resource. You can search for `partsunlimited-web` **(1)** to find your Web App and App Service Plan.

   ![The search box for the resource is filled in with partsunlimited-web. The partsunlimited-web-20 Azure App Service is highlighted in the list of resources in the hands-on-lab-SUFFIX resource group.](media/resource-group-appservice-resource.png "Resources")

1. Select **URL** and navigate to the Parts Unlimited web site hosted in Azure App Service.

    ![Parts Unlimited App Service is on screen. URL is highlighted.](media/navigate-to-parts-unlimited-app-service.png "App Service Public Endpoint")

1. Select **Login (1)**. If a login wasn't created in the earlier exercise then select **Register as a new user? (2)**, otherwise skip to step 6 (login to the web site)

    ![Parts Unlimited web site login screen is presented. Log in and Register as a new user buttons are highlighted.](media/register-parts-unlimited.png "Parts Unlimited Login")

1. Type in `test@test.com` for the email **(1)** and `Password.1!!` **(2)** for the password. Select **Register (3)**.

    ![Parts Unlimited web site user registration screen is presented. Email box is filled with test@test.com. Password boxes are filled in with Password.1!!. The register button is highlighted.](media/register-parts-unlimited-new-user.png "Register")

1. On the next screen, select **Click here to confirm your email** to confirm your e-mail.

1. Select **Login (1)**, type the credentials listed below and click the **Login (4)** button.

    - **Email (2):** test@test.com
    - **Password (3):** Password.1!!

    ![Parts Unlimited web site login screen is presented. Email box is filled with test@test.com. Password boxes are filled in with Password.1!!. Login button is highlighted. ](media/parts-umlimited-login.png "Login")

1. Select a product from the home page, and select **Add to Card** once you are on the product detail page.

    ![Product detail page is shown. Add to cart button is highlighted.](media/parts-unlimited-add-to-cart.png "Add to Cart")

1. Select **Checkout** on the next screen.

1. Fill in sample shipping information **(1)** for testing purposes. Use coupon code **FREE (2)** and select **Submit Order (3)**.

    ![Sample shipping information is filled in. FREE coupon code is typed in. Submit Order button is highlighted.](media/parts-unlimited-order.png "Submit Order")

1. Once checkout is complete select **view your order** to see order details.

    ![Checkout Complete page is shown. View your order link is highlighted.](media/parts-unlimited-view-order-details.png "View your order")

1. Observe the invoice field. Right now, your order is flagged as in processing. An order job is submitted to the Azure Storage Queue to be processed by Azure Functions. Refresh the page every 15 seconds to see if anything changes about your order.

    ![Order details page is open. Invoice field is highlighted.](media/parts-unlimited-invoice-processing.png "Invoice processing")

1. Once your order has been processed, an invoice will be created, and a download link will appear. Select the download link to download the PDF invoice created for your order by Azure Functions.

    ![Order details page is open. Invoice field is highlighted to show a download link.](media/parts-unlimited-pdf-download.png "Invoice download")

    Here is your invoice.

    ![A sample Parts Unlimited Invoice is presented.](media/invoice-pdf.png "Sample Invoice")

## Task 4: Enable Application Insights on the Function App

In this task, you add Application Insights to your Function App in the Azure Portal, to be able to collect insights related to Function executions.

1. In the [Azure portal](https://portal.azure.com), navigate to your **Function App** by selecting **Resource groups** from Azure services list, selecting the **hands-on-lab-SUFFIX** resource group, and selecting the **parts-func-{uniquesuffix}** App service from the list of resources.

   ![The Function App resource is highlighted in the list of resources.](media/azure-resources-function-app.png "Function App")

1. On the Function App blade, select **Application Insights (1)** under Settings from the left-hand menu. On the Application Insights blade, select **Turn on Application Insights (2)**.

   ![Application Insights blade is selected. The Turn on Application Insights button is highlighted.](media/function-app-add-app-insights.png "Turn on Application Insights for Function App")

1. On the Application Insights blade, select **Create new resource (1)**, accept the default name provided, and then select **Apply (2)**. Select **Yes (3)** when prompted about restarting the Function App to apply monitoring settings.

   ![The Create New Application Insights blade is displayed with a unique name set under Create new resource. Apply and the following Yes approval buttons are highlighted.](media/function-app-app-insights.png "Add Application Insights")

1. After the Function App restarts, select **View Application Insights data**.

   ![The View Application Insights data link is highlighted.](media/function-app-view-application-insights-data.png "View Application Insights data")

1. On the Application Insights blade, select **Live Metrics Stream (1)** from the left-hand menu.

   ![Live Metrics Stream is highlighted in the left-hand menu on the Application Insights blade.](media/app-insights-live-metrics-stream.png "Application Insights")

   > While having Live Metric up, try submitting a new order on the Parts Unlimited web site. You will see access to blob storage in the telemetry to upload the PDF **(2)** and execution count on the graph **(3)**.
