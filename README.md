# Azure-Security-and-Monitoring
## Project Overview
This project demonstrates the deployment of a **MEAN (MongoDB, Express.js, Angular, Node.js)** application using various **Azure services**. Additionally, it includes the creation of a **monitoring dashboard** to visualize and analyze application statistics effectively.

## Objectives
- Deploy a fully functional **MEAN** application using **Azure services**.
- Ensure **scalability** and **reliability** by leveraging Azure's cloud infrastructure.
- Create a **monitoring dashboard** to provide insights into application performance and usage statistics.

## Prerequisites
- An **active Azure account**.
- A functional **MEAN application** ready for deployment.
- Basic understanding of **Azure services**.
- **Azure CLI** installed and configured on your local machine.
- Familiarity with monitoring tools such as **Azure Monitor** and **Application Insights**.

## Deployment Steps

### 1. Set Up Azure Resources
#### Create a Resource Group
```sh
az group create --name <ResourceGroupName> --location <Region>
```

#### Provision Virtual Machines (if required)
```sh
az vm create --resource-group <ResourceGroupName> --name <VMName> --image UbuntuLTS --admin-username <Username> --generate-ssh-keys
```

#### Deploy Node.js and Angular Applications using Azure App Service
```sh
az appservice plan create --name <AppServicePlanName> --resource-group <ResourceGroupName> --sku F1
az webapp create --name <WebAppName> --resource-group <ResourceGroupName> --plan <AppServicePlanName>
```

#### Set Up Azure Cosmos DB (MongoDB API)
```sh
az cosmosdb create --name <CosmosDBName> --resource-group <ResourceGroupName> --kind MongoDB
```

### 2. Deploy the MEAN Application

#### Deploy Backend (Node.js)
```sh
cd backend
npm install
az webapp up --name <WebAppName> --resource-group <ResourceGroupName> --runtime "NODE|14-lts"
```

#### Deploy Frontend (Angular)
```sh
cd frontend
ng build --prod
az storage account create --name <StorageAccountName> --resource-group <ResourceGroupName> --location <Region> --sku Standard_LRS
az storage blob service-properties update --account-name <StorageAccountName> --static-website --index-document index.html
az storage blob upload-batch -d '$web' --account-name <StorageAccountName> -s ./dist/<ProjectName>
```

#### Configure Database Connection (MongoDB - Azure Cosmos DB)
```sh
CONNECTION_STRING=$(az cosmosdb list-connection-strings --name <CosmosDBName> --resource-group <ResourceGroupName> --query connectionStrings[0].connectionString -o tsv)
```

### 3. Configure Networking and Security

#### Enable Application Gateway or Azure Front Door for Traffic Management
```sh
az network application-gateway create --name <GatewayName> --resource-group <ResourceGroupName> --sku Standard_v2 --location <Region> --public-ip-address <PublicIPName>
```

#### Configure Network Security Groups (NSGs)
```sh
az network nsg create --name <NSGName> --resource-group <ResourceGroupName>
```

#### Assign Managed Identity to Web App for Secure Resource Access
```sh
az webapp identity assign --name <WebAppName> --resource-group <ResourceGroupName>
```

### 4. Set Up Monitoring Dashboard

#### Enable Azure Monitor and Application Insights
```sh
az monitor log-analytics workspace create --resource-group <ResourceGroupName> --workspace-name <WorkspaceName>
az monitor app-insights component create --app <AppName> --location <Region> --resource-group <ResourceGroupName>
```

#### Create Custom Dashboards in Azure Portal
- **CPU and memory usage**
- **API response times**
- **Database query performance**
- **Error and exception tracking**

#### Integrate Azure Log Analytics for Advanced Querying
```sh
az monitor log-analytics query --workspace <WorkspaceName> --analytics-query "<KQL Query>"
```

## Reference Link
For detailed guidance and additional tips, refer to the following repository: **[ResumeAI GitHub Repository](#)**

## Submission Instructions
- Ensure that the **MEAN application** is fully deployed and accessible via a **public endpoint**.
- Provide **screenshots** of the deployed application and the monitoring dashboard.
- Push all relevant **code and documentation** to a **GitHub repository**.
- Share the **repository link** for submission.

## Conclusion
By following the above steps, you will have successfully deployed a **MEAN application** using **Azure services**, while ensuring **effective monitoring and performance tracking**. This setup not only showcases your **technical skills** but also demonstrates your ability to **leverage cloud infrastructure effectively**.

