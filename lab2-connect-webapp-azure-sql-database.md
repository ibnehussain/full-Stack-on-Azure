# Lab 2: Connect Azure App Service to Azure SQL Database

## Objective
Configure an Azure-hosted .NET Web App to connect securely to an Azure SQL Database.

---

## Prerequisites
- **Azure App Service deployed successfully**: Ensure your web app is running and accessible.
- **Azure SQL Server and Database created**: Verify that the database is online.
- **SQL authentication enabled**: Ensure you have a valid username and password.
- **Firewall access configured**: Allow Azure services and your IP to access the database.

> **Tip:** Use the Azure Portal to verify that your database and server are configured correctly.

---

## Lab Scenario
Your web application needs to store and retrieve data from a managed relational database hosted in Azure. This lab will guide you through connecting your Azure App Service to an Azure SQL Database securely.

---

## Quick Start (Optional)
If you want to get started quickly with a sample application, you can clone this repository:

```bash
git clone https://github.com/ibnehussain/accapp001.git
```

This repository contains a pre-configured .NET application that you can use as a starting point for this lab.

> **Note:** After cloning, you'll still need to follow the steps below to configure the database connection for your specific Azure resources.

---

## Steps

### Step 1: Verify Azure SQL Database
1. **Open Azure Portal**:
   - Navigate to the **Azure SQL Database** resource.
2. **Check database status**:
   - Ensure the database is **online** and accessible.
3. **Firewall settings**:
   - Verify that the firewall allows connections from Azure services and your IP address.

> **Note:** If the database is not accessible, review the firewall rules and ensure the server is running.

---

### Step 2: Retrieve Database Connection String
1. **Navigate to Connection Strings**:
   - Open the Azure SQL Database resource in the Azure Portal.
2. **Copy the ADO.NET connection string**:
   - This string contains the server name, database name, and authentication details.
3. **Secure credentials**:
   - Store the connection string securely, avoiding hardcoding it in your application.

> **Tip:** Use Azure Key Vault to securely manage and access sensitive information like connection strings.

---

### Step 3: Configure App Service Settings
1. **Open App Service Configuration**:
   - Navigate to your Azure App Service in the Azure Portal.
2. **Add a new Connection String**:
   - Go to the **Configuration** section and add a new connection string.
   - Set the **type** to **SQLAzure**.
3. **Save and restart**:
   - Save the changes and restart the App Service to apply the new settings.

> **Best Practice:** Use descriptive names for connection strings to make them easily identifiable.

---

### Step 4: Validate Connectivity
1. **Access the web application**:
   - Open the deployed application in a browser.
2. **Test database operations**:
   - Verify that the application can perform data operations like reading and writing.
3. **Monitor logs**:
   - Check the application logs in the Azure Portal for any connectivity issues.

> **Troubleshooting:** If connectivity fails, ensure the connection string is correct and the database is accessible.

---

## Validation
- **Successful connection**: Verify that the application connects to the Azure SQL Database without errors.
- **Data operations**: Ensure that data can be retrieved and stored successfully.
- **Secure configuration**: Confirm that no connection strings are hardcoded in the application code.

> **Tip:** Use Azure Monitor to track database performance and identify potential issues.

---

## Key Takeaways
- **Secure Integration**: Azure App Service integrates securely with Azure SQL Database.
- **Connection Strings**: Store connection strings in App Settings for better security.
- **Managed Services**: Azure handles database availability, scaling, and maintenance, allowing you to focus on application development.

> **Next Steps:** Explore advanced features like Azure Managed Identity for even more secure database access.