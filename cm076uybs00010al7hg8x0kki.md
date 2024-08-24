---
title: "Deploying a web app with ARM templates and Azure CLI.  A Comprehensive Guide."
seoTitle: "Azure ARM Templates"
seoDescription: "Azure ARM Templates"
datePublished: Tue Aug 20 2024 23:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm076uybs00010al7hg8x0kki
slug: deploying-a-web-app-with-arm-templates-and-azure-cli-a-comprehensive-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724446224271/6f384256-851d-4374-9508-cf63568fa065.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1724446312952/6f47ea31-c925-470b-b067-02348c6c90d6.png
tags: azure-devops, azure-cli, arm-template

---

In today’s fast-paced world of cloud computing, deploying and managing resources efficiently is crucial. Azure provides two powerful tools for automating deployments: **Azure Resource Manager (ARM) templates** and the **Azure CLI**. Together, they offer a flexible, repeatable, and scriptable way to deploy infrastructure and applications in the Azure cloud.

In this blog, we’ll explore how ARM templates and Azure CLI can be used to deploy an Azure Web App and ensure a smooth, automated cloud deployment experience.

### **What is an ARM Template?**

An **Azure Resource Manager (ARM) template** is a JSON file that defines the resources you want to deploy to your Azure environment. It allows for Infrastructure-as-Code (IaC), which means you can programmatically define and manage your Azure resources. ARM templates support:

* **Idempotency**: Deploy the same template multiple times without duplicating resources.
    
* **Consistency**: Deploy the same configurations across environments, ensuring uniformity.
    
* **Version control**: Store templates in version-controlled repositories, allowing rollbacks and consistent deployment.
    

### **Key Components of an ARM Template:**

1. **Schema**: Defines the structure and properties of the template.
    
2. **Content Version**: Tracks the version of the template.
    
3. **Parameters**: Allow for dynamic values to be passed during deployment (e.g., names, regions).
    
4. **Resources**: The actual Azure services (VMs, web apps, databases, etc.) to be deployed.
    
5. **Outputs**: Return values from the deployment, such as URLs or resource IDs.
    

### **What is Azure CLI?**

The **Azure CLI** is a command-line tool that allows you to interact with Azure services using simple commands. It is ideal for automation and scripting tasks like deploying ARM templates, managing resources, and querying Azure services. Azure CLI can be used in local terminals, cloud shell, or integrated with CI/CD pipelines.

### **ARM Templates vs. Azure CLI: Why Use Both?**

While ARM templates define infrastructure and services declaratively, Azure CLI allows for the procedural execution of tasks. Here’s how they complement each other:

* **ARM templates** provide a static, repeatable way to describe your infrastructure.
    
* **Azure CLI** provides dynamic control, allowing you to customise, automate, and monitor deployments.
    

In tandem, ARM templates and Azure CLI give you full control over the automation of your cloud infrastructure.

### **Deploying a Web App with ARM Templates and Azure CLI: A Step-by-Step Guide.**

Now, let’s dive into a real-world example where we deploy an Azure Web App using an ARM template and the Azure CLI.

### Prerequisites:

* Install the Azure CLI.
    
* Ensure you have an active Azure account and subscription.
    
* Create or identify an HTML template for your website (we'll use a full website in this example).
    
* Install Visual Studio Code or any code editor.
    
* **Step 1: Install the Azure CLI**
    
    First, ensure you have the [Azure CLI installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). You can also use the Azure Cloud Shell for this exercise, as it comes pre-installed with Azure CLI.
    
    Run the following command to log in to your Azure account:
    
    ```bash
    az login
    ```
    
    #### **Step 2: Create a Resource Group**
    
    Resource groups in Azure allow you to organize and manage resources collectively. Use the following command to create one:
    
    ```bash
    az group create --name myWebAppRG --location eastus
    ```
    

#### **Step 3: Define an ARM Template**

Create an `azuredeploy.json` file that describes the Azure Web App you want to deploy. Below is a simple ARM template that creates a Web App and App Service Plan:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "webAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Web App to be created."
      }
    },
    "appServicePlanName": {
      "type": "string",
      "metadata": {
        "description": "Name of the App Service Plan."
      }
    },
    "location": {
      "type": "string",
      "defaultValue": "East US",
      "metadata": {
        "description": "Location for all resources."
      }
    },
    "skuName": {
      "type": "string",
      "defaultValue": "F1",
      "allowedValues": [
        "F1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3"
      ],
      "metadata": {
        "description": "The pricing tier for the App Service Plan."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Web/serverfarms",
      "apiVersion": "2021-02-01",
      "name": "[parameters('appServicePlanName')]",
      "location": "[parameters('location')]",
      "sku": {
        "name": "[parameters('skuName')]",
        "tier": "[if(equals(parameters('skuName'), 'F1'), 'Free', 'Basic')]",
        "capacity": 1
      },
      "properties": {}
    },
    {
      "type": "Microsoft.Web/sites",
      "apiVersion": "2021-02-01",
      "name": "[parameters('webAppName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('appServicePlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', parameters('appServicePlanName'))]"
      }
    }
  ],
  "outputs": {
    "webAppUrl": {
      "type": "string",
      "value": "[concat('https://', reference(resourceId('Microsoft.Web/sites', parameters('webAppName'))).defaultHostName)]",
      "metadata": {
        "description": "The URL of the deployed Web App."
      }
    }
  }
}
```

This ARM template will deploy:

* A web app named `webAppName`
    
* An App Service Plan in the `Free` tier
    

#### **Step 4: Create the Parameters File**

Create an `azuredeploy.parameters.json` file to pass dynamic values to the ARM template:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "webAppName": {
      "value": "myBeautifulWebApp"
    },
    "appServicePlanName": {
      "value": "myAppServicePlan"
    },
    "location": {
      "value": "East US"
    },
    "skuName": {
      "value": "F1"
    }
  }
}
```

#### **Step 5: Deploy the ARM Template via Azure CLI**

Now that we have the ARM template and parameters file ready, we can deploy the template using the following command:

```bash
az deployment group create \
  --resource-group WebAppResourceGroup \
  --template-file azuredeploy.json \
  --parameters azuredeploy.parameters.json
```

This will create the web app and app service plan in Azure.

#### **Step 6: Push Your Website Code to GitHub**

To deploy content to the web app, you can push your HTML/CSS/JavaScript files to a GitHub repository and connect it to your web app.

Here’s an example of how to connect a GitHub repo to your web app using the Azure CLI:

```bash
az webapp deployment source config --name myBeautifulWebApp \
  --resource-group myWebAppRG \
  --repo-url https://github.com/laoluafolami/myportfolio.git \
  --branch master --manual-integration
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724435484934/ef29771c-4466-4979-a00d-40f6e7abc0f4.png align="center")

#### **Step 7: Browse Your Deployed Web App**

Once the deployment is complete, retrieve the URL of your web app:

```bash
az webapp show --resource-group myWebAppRG --name myBeautifulWebApp --query defaultHostName -o tsv
```

Paste the URL in your browser to see your deployed website!

[The deployed website URL](http://mybeautifulwebapp.azurewebsites.net)

[mybeautifulwebapp.azurewebsites.net](http://mybeautifulwebapp.azurewebsites.net)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724435624545/4330585c-1590-4b32-bfeb-0441816c28d4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1724435819549/07d68dda-e186-4767-88eb-754c20311323.png align="center")

### **Benefits of Using ARM Templates and Azure CLI**

1. **Automation**: No more manual clicks in the Azure portal. Templates and CLI scripts make it easy to automate deployments.
    
2. **Reusability**: ARM templates can be reused across different environments, ensuring consistency.
    
3. **Scalability**: With ARM templates, you can deploy a single web app or an entire architecture involving multiple services like databases, VMs, and networks.
    
4. **Versioning and Rollbacks**: Store your templates in GitHub or another version control system for better management and rollback capabilities.
    

---

### **Conclusion**

Using ARM templates and Azure CLI provides a robust and scalable way to manage your Azure infrastructure. With these tools, you can deploy consistent, version-controlled infrastructure, automate processes, and reduce errors associated with manual configurations. The combination of ARM templates and Azure CLI should be an integral part of your cloud operations toolkit, enabling smooth and reliable deployments.

By adopting Infrastructure-as-Code practices, you ensure better control, efficiency, and scalability for your cloud resources. Whether you’re managing a small web app or a complex cloud architecture, ARM templates and Azure CLI can help you do it in a structured and automated way.

---

**Happy Cloud Deployment!**