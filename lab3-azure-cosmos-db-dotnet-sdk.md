---

# 🧪 Lab

## Create Azure Cosmos DB & Perform CRUD Using .NET SDK

### 🎯 Lab Objective
By the end of this lab, learners will be able to:

- Create an **Azure Cosmos DB (SQL API)** account
- Create a **Database and Container**
- Use the **.NET SDK** to perform **Create, Read, Update, Delete (CRUD)** operations
- Understand **partition keys** in practice
- Implement **error handling** and **best practices**
- Perform **advanced queries** and **pagination**

---

## 🧰 Prerequisites

- Azure Subscription
- Visual Studio 2022 (or VS Code)
- .NET 8 SDK installed
- Basic C# knowledge
- Familiarity with Azure Portal

---

## 🧩 Architecture Overview

```plaintext
.NET Console App
     |
     v
Cosmos DB (SQL API)
  └── Database
       └── Container (/department)
```

---

# 🪜 LAB STEPS

---

## STEP 1️⃣ – Create Azure Cosmos DB Account

1. Go to **Azure Portal**
2. Click **Create a resource**
3. Search **Azure Cosmos DB**
4. Select **Azure Cosmos DB for NoSQL**
5. Click **Create**

### Configuration

| Setting         | Value                   |
| --------------- | ----------------------- |
| Account Name    | cosmoslab<unique>       |
| API             | NoSQL                   |
| Location        | Any Region              |
| Capacity mode   | Provisioned throughput  |
| Apply Free Tier | No                      |

6. Click **Review + Create → Create**

⏳ Wait for deployment to complete.

> **Why this step?**
> Azure Cosmos DB is a globally distributed, multi-model database service. Creating an account is the first step to leverage its capabilities.

---

## STEP 2️⃣ – Create Database & Container

1. Open the Cosmos DB account
2. Go to **Data Explorer**
3. Click **New Database**

   - Database Name: `EmployeeDB`
   - Throughput: `400 RU/s`
4. Click **New Container**

   - Container Name: `Employees`
   - Partition Key: `/department`
   - Throughput: `400 RU/s`

> **Why this step?**
> Partition keys ensure data distribution and scalability. Choosing `/department` as the partition key helps group related data.

---

## STEP 3️⃣ – Get Connection Details

1. Go to **Settings → Keys**
2. Copy:

   - **URI**
   - **Primary Key**

📌 You will use these in your .NET app.

---

## STEP 4️⃣ – Create .NET Console Application

### Using VS Code

1. Open **VS Code**.
2. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac) to open the Command Palette.
3. Type `> .NET: Generate Assets for Build and Debug` and select it.
4. Create a new folder for your project and open it in VS Code.
5. Open the integrated terminal (`Ctrl+``) and run the following command to create a new console application:

   ```bash
   dotnet new console -n CosmosCrudDemo
   ```

6. Navigate to the newly created project folder:

   ```bash
   cd CosmosCrudDemo
   ```

7. Open the `Program.cs` file to start coding.

> **Why this step?**
> VS Code provides a lightweight and flexible environment for developing .NET applications.

---

## STEP 5️⃣ – Install Cosmos DB SDK

Open **Package Manager Console** and run:

```powershell
Install-Package Microsoft.Azure.Cosmos
```

> **Why this step?**
> The SDK provides APIs to interact with Cosmos DB.

---

## STEP 6️⃣ – Create Model Class

Create a file **Employee.cs**

```csharp
using Newtonsoft.Json;

public class Employee
{
    [JsonProperty("id")]
    public string Id { get; set; }

    public string Name { get; set; }
    public string Department { get; set; }
    public int Salary { get; set; }
}
```

> **Best Practice:** Use `JsonProperty` to map C# properties to JSON fields.

---

## STEP 7️⃣ – Initialize Cosmos Client

Open **Program.cs**

```csharp
using Microsoft.Azure.Cosmos;

string endpoint = "<YOUR_COSMOS_URI>";
string key = "<YOUR_PRIMARY_KEY>";

string databaseId = "EmployeeDB";
string containerId = "Employees";

CosmosClient client = new CosmosClient(endpoint, key);
Container container = client.GetContainer(databaseId, containerId);
```

> **Why this step?**
> The `CosmosClient` is the entry point for interacting with Cosmos DB.

---

## STEP 8️⃣ – CREATE Item (Insert)

```csharp
try
{
    Employee emp = new Employee
    {
        Id = Guid.NewGuid().ToString(),
        Name = "Azhar",
        Department = "IT",
        Salary = 1000
    };

    ItemResponse<Employee> response =
        await container.CreateItemAsync(emp, new PartitionKey(emp.Department));

    Console.WriteLine($"Created Employee: {response.Resource.Name}");
}
catch (CosmosException ex)
{
    Console.WriteLine($"Error: {ex.StatusCode} - {ex.Message}");
}
```

> **Best Practice:** Always handle exceptions to ensure robust applications.

---

## STEP 9️⃣ – READ Item

```csharp
try
{
    ItemResponse<Employee> readResponse =
        await container.ReadItemAsync<Employee>(
            emp.Id,
            new PartitionKey(emp.Department));

    Console.WriteLine($"Read Employee: {readResponse.Resource.Name}");
}
catch (CosmosException ex)
{
    Console.WriteLine($"Error: {ex.StatusCode} - {ex.Message}");
}
```

---

## STEP 🔟 – UPDATE Item

```csharp
try
{
    emp.Salary = 90000;

    ItemResponse<Employee> updateResponse =
        await container.ReplaceItemAsync(
            emp,
            emp.Id,
            new PartitionKey(emp.Department));

    Console.WriteLine($"Updated Salary: {updateResponse.Resource.Salary}");
}
catch (CosmosException ex)
{
    Console.WriteLine($"Error: {ex.StatusCode} - {ex.Message}");
}
```

---

## STEP 1️⃣1️⃣ – DELETE Item

```csharp
try
{
    await container.DeleteItemAsync<Employee>(
        emp.Id,
        new PartitionKey(emp.Department));

    Console.WriteLine("Employee deleted");
}
catch (CosmosException ex)
{
    Console.WriteLine($"Error: {ex.StatusCode} - {ex.Message}");
}
```

---

## STEP 1️⃣2️⃣ – Advanced Querying

### Query with SQL

```csharp
var sqlQuery = "SELECT * FROM c WHERE c.Department = 'IT'";
var query = container.GetItemQueryIterator<Employee>(new QueryDefinition(sqlQuery));

while (query.HasMoreResults)
{
    foreach (var employee in await query.ReadNextAsync())
    {
        Console.WriteLine($"Employee: {employee.Name}, Salary: {employee.Salary}");
    }
}
```

> **Why this step?**
> SQL queries allow flexible data retrieval.

---

# 🧠 Key Learning Points

- Partition key **must be supplied** for Read/Update/Delete
- Cosmos DB is **schema-less**
- RU/s affects performance & cost
- SDK handles JSON serialization automatically
- Exception handling ensures reliability

For detailed guidance on using the Azure Cosmos DB .NET SDK, including advanced features, best practices, and troubleshooting tips, visit the official documentation:
https://learn.microsoft.com/en-us/azure/cosmos-db/sdk-dotnet-v3

---

## 🧪 Optional Challenges

- Convert app to **ASP.NET Web API**
- Use **Managed Identity** for authentication
- Implement **retry policies** for transient errors

---

