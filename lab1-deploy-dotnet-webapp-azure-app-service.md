# Lab 1: Create & Deploy a .NET Web App to Azure App Service

## Objective
Deploy a .NET Web Application to Azure App Service using Platform as a Service (PaaS).

---

## Prerequisites
- **Active Azure subscription**: Ensure you have access to the Azure Portal.
- **Visual Studio**: Install Visual Studio with the following workloads:
  - .NET desktop development
  - Azure development
- **Basic understanding of Azure Portal**: Familiarity with creating resources and navigating the portal.
- **Internet access**: Required for downloading dependencies and deploying the app.

> **Tip:** If you don’t have an Azure subscription, you can create a free account with $200 in credits at [Azure Free Account](https://azure.microsoft.com/free/).

---

## Lab Scenario
You are building a cloud-based web application and want to host it using Azure App Service so that infrastructure management is handled by Azure. This lab will guide you through creating, deploying, and validating your application.

---

## Steps

### Step 1: Create a .NET Web Application
1. **Open Visual Studio**:
   - Launch Visual Studio and ensure you are signed in with your Microsoft account.
2. **Create a new project**:
   - Select **ASP.NET Core Web Application**.
   - Choose the **Razor Pages** template.
3. **Configure the project**:
   - Use the default project settings (e.g., Framework: .NET 6 or later).
4. **Run the application locally**:
   - Press `F5` to build and run the application.
   - Verify that the application launches in your default browser without errors.

> **Note:** Ensure all dependencies are restored before running the application.

---

### Step 2: Create Azure App Service
1. **Start the Publish workflow**:
   - In Visual Studio, right-click the project in **Solution Explorer** and select **Publish**.
2. **Choose Azure as the target**:
   - Select **Azure App Service (Windows)**.
3. **Create a new App Service**:
   - Provide the following details:
     - **Resource Group**: Create a new or select an existing resource group.
     - **App Service Plan**: Choose a pricing tier that fits your needs (e.g., Free or Basic).
     - **Region**: Select a region close to your users.
     - **Runtime stack**: Ensure it matches your application’s framework (e.g., .NET 6).

> **Tip:** Use meaningful names for your resources to make them easier to identify later.

---

### Step 3: Deploy the Application
1. **Publish the application**:
   - Click **Publish** in Visual Studio to deploy the application to Azure.
2. **Monitor the deployment**:
   - Wait for the deployment process to complete. This may take a few minutes.
3. **Access the deployed application**:
   - Once deployed, Visual Studio will provide the URL of your web app.
   - Open the URL in a browser to verify the deployment.

> **Troubleshooting:** If the deployment fails, check the **Output** window in Visual Studio for detailed error messages.

---

## Validation
- **Application loads successfully**: Verify that the application is accessible from the Azure App Service URL.
- **No errors**: Ensure there are no runtime errors or missing assets.
- **Public accessibility**: Confirm that the app is accessible from any device with internet access.

> **Tip:** Bookmark the app URL for quick access during future testing.

---

## Key Takeaways
- **Azure App Service**: A fully managed PaaS offering that simplifies web app hosting.
- **Visual Studio Integration**: Deployment can be done directly from Visual Studio, streamlining the process.
- **No server management**: Azure handles server and OS management, allowing you to focus on your application.

> **Next Steps:** Explore additional Azure services like Azure SQL Database or Azure Functions to enhance your application.