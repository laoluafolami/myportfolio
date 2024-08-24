---
title: "Deploy Virtual Machines Using ARM Templates: A Complete Guide."
datePublished: Tue Aug 13 2024 01:51:15 GMT+0000 (Coordinated Universal Time)
cuid: clzrrntv8000309l8aj2xhw7k
slug: deploy-virtual-machines-using-arm-templates-a-complete-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723513501957/89ffe561-dd2d-494a-bdfb-8d33a988d31e.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723513866474/3bf0c812-0303-45af-8825-2ea1e1370483.png
tags: azure, arm-templates

---

### **Introduction**

Azure Resource Manager (ARM) templates are JSON files that define the infrastructure and configuration of Azure resources. They enable the deployment of resources in a consistent, repeatable manner, making it easier to manage and scale cloud infrastructure. Here are key points about ARM templates:

### Understanding Azure Resource Manager

Azure Resource Manager (ARM) is the deployment and management service for Azure. It provides a consistent management layer that enables you to create, update, and delete resources in your Azure account.

ARM allows you to manage your infrastructure through declarative templates rather than scripts.

### Key Features

* **Declarative Syntax**: ARM templates use a declarative syntax, meaning you specify *what* you want to deploy without having to write the sequence of commands to deploy resources. Azure handles the deployment process based on the specified configuration.
    
* **Infrastructure as Code**: ARM templates enable you to define and deploy infrastructure as code (IaC). This approach allows for version control, collaboration, and integration with CI/CD pipelines, enhancing DevOps practices.
    
* **Idempotency**: Deployments using ARM templates are idempotent. This means that the same template can be applied multiple times without changing the existing state of the resources, ensuring consistent deployment results.
    
* **Parameterization**: Templates can be parameterized, allowing you to provide different inputs for different environments (e.g., development, staging, production) without changing the template itself. Parameters make templates reusable and flexible.
    
* **Modularity**: ARM templates support modular design through linked and nested templates, enabling complex infrastructure setups by combining simpler, modular templates. This approach promotes reusability and simplifies management.
    
* **Resource Group Scope**: ARM templates are scoped to resource groups, enabling you to deploy and manage resources in an isolated environment. This isolation helps with organizing resources and controlling access.
    
* **Dependency Management**: ARM templates can specify dependencies between resources, ensuring that resources are deployed in the correct order. Azure automatically manages these dependencies during deployment.
    
    ### Benefits
    
* **Consistency**: Templates ensure that deployments are consistent across different environments and reduce the risk of human error.
    
* **Scalability**: They simplify scaling infrastructure by allowing you to define resources once and deploy them multiple times.
    
* **Automation**: ARM templates can be integrated into CI/CD pipelines for automated deployments, reducing manual intervention.
    
* **Cost Management**: By defining all resources in a template, you can easily track and manage the costs associated with your infrastructure.
    

### Best Practices

* **Use Source Control**: Store your ARM templates in a source control system to track changes, collaborate with team members, and manage versions.
    
* **Validate Templates**: Use tools like Azure Resource Manager Template Toolkit (ARM-TTK) and Visual Studio Code extensions to validate your templates before deployment.
    
* **Modularize Templates**: Break down large templates into smaller, manageable components for better reusability and maintainability.
    
* **Parameterize**: Use parameters to make templates flexible and adaptable to different environments and scenarios.
    

### Prerequisites

Before you begin, ensure you have the following:

* **Azure Subscription**: You need an active Azure subscription. If you don’t have one, you can create a free account on the Azure website.
    
* **Azure CLI or PowerShell**: Make sure you have Azure CLI or PowerShell installed and configured with your Azure account.
    
* **Basic Knowledge of JSON**: Since ARM templates are written in JSON, understanding the basics of JSON will help.
    

### Step 1: Understanding the ARM Template Structure

An ARM template consists of several sections:

* `$schema`: Specifies the location of the JSON schema file that describes the version of the template language.
    
* `contentVersion`: Defines the version of the template (arbitrary for user reference).
    
* `parameters`: Contains all the values that can be passed to the template during deployment.
    
* `variables`: Defines values that can be used throughout the template, calculated from parameters or other variables.
    
* `resources`: Specifies the resources to be deployed or updated in the Azure environment.
    
* `outputs`: Specifies any values you wish to retrieve after the deployment is complete.
    

* ## Step 2: Creating the ARM Template
    
    Let’s create an ARM template for a simple Windows VM.
    
    1. **Define the Basic Template Structure**:
        
        Create a JSON file named `azuredeploy.json` and start with the basic structure:
        
        ```json
        {
          "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {}
        }
        ```
        
    2. **Add Parameters**:
        
    
    Parameters make your template flexible and reusable. Here, we’ll add parameters for the VM name, admin username, and admin password.
    
* ```json
    "parameters": {
      "vmName": {
        "type": "string",
        "defaultValue": "myVM",
        "metadata": {
          "description": "Name of the virtual machine"
        }
      },
      "adminUsername": {
        "type": "string",
        "metadata": {
          "description": "Admin username"
        }
      },
      "adminPassword": {
        "type": "secureString",
        "metadata": {
          "description": "Admin password"
        }
      }
    }
    ```
    

3. **Define the VM Resource**:
    

In the `resources` section, add a resource definition for the VM.

```json
"resources": [
  {
    "type": "Microsoft.Compute/virtualMachines",
    "apiVersion": "2022-11-01",
    "name": "[parameters('vmName')]",
    "location": "[resourceGroup().location]",
    "properties": {
      "hardwareProfile": {
        "vmSize": "Standard_DS1_v2"
      },
      "osProfile": {
        "computerName": "[parameters('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
      },
      "storageProfile": {
        "imageReference": {
          "publisher": "MicrosoftWindowsServer",
          "offer": "WindowsServer",
          "sku": "2019-Datacenter",
          "version": "latest"
        },
        "osDisk": {
          "createOption": "FromImage"
        }
      },
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(parameters('vmName'), '-nic'))]"
          }
        ]
      }
    }
  }
]
```

4. **Add Additional Resources**:
    

If needed, add additional resources like network interfaces, public IPs, or storage accounts to the `resources` section.

## **The complete JSON ARM template:**

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "vmName": {
      "type": "string",
      "defaultValue": "myWindowsVM",
      "metadata": {
        "description": "Name of the virtual machine."
      }
    },
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Admin username for the virtual machine."
      }
    },
    "adminPassword": {
      "type": "secureString",
      "metadata": {
        "description": "Admin password for the virtual machine."
      }
    },
    "vmSize": {
      "type": "string",
      "defaultValue": "Standard_DS1_v2",
      "metadata": {
        "description": "Size of the virtual machine."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat('vhd', uniqueString(resourceGroup().id))]",
    "nicName": "[concat(parameters('vmName'), '-nic')]",
    "ipName": "[concat(parameters('vmName'), '-ip')]",
    "vnetName": "myVnet",
    "subnetName": "default",
    "subnetRef": "[resourceId('Microsoft.Network/virtualNetworks/subnets', variables('vnetName'), variables('subnetName'))]",
    "ipConfigName": "ipconfig1"
  },
  "resources": [
    {
      "type": "Microsoft.Network/publicIPAddresses",
      "apiVersion": "2022-01-01",
      "name": "[variables('ipName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic"
      }
    },
    {
      "type": "Microsoft.Network/virtualNetworks",
      "apiVersion": "2022-01-01",
      "name": "[variables('vnetName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "10.0.0.0/16"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "10.0.0.0/24"
            }
          }
        ]
      }
    },
    {
      "type": "Microsoft.Network/networkInterfaces",
      "apiVersion": "2022-01-01",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Network/publicIPAddresses', variables('ipName'))]",
        "[resourceId('Microsoft.Network/virtualNetworks', variables('vnetName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "[variables('ipConfigName')]",
            "properties": {
              "subnet": {
                "id": "[variables('subnetRef')]"
              },
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('ipName'))]"
              }
            }
          }
        ]
      }
    },
    {
      "type": "Microsoft.Compute/virtualMachines",
      "apiVersion": "2022-11-01",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Network/networkInterfaces', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[parameters('vmSize')]"
        },
        "osProfile": {
          "computerName": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2019-Datacenter",
            "version": "latest"
          },
          "osDisk": {
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('nicName'))]"
            }
          ]
        }
      }
    }
  ],
  "outputs": {
    "vmName": {
      "type": "string",
      "value": "[parameters('vmName')]"
    },
    "adminUsername": {
      "type": "string",
      "value": "[parameters('adminUsername')]"
    }
  }
}
```

### Step 3: Deploying the ARM Template

You can deploy your ARM template using ***Azure CLI*** or ***PowerShell.***

**Using Azure Command-Line Interface (CLI)**

The Azure Command-Line Interface (CLI) is a cross-platform command-line tool that can be installed locally on Windows computers. You can use the Azure CLI for Windows to connect to Azure and execute administrative commands on Azure resources. The Azure CLI for Windows can also be used from a browser through the Azure Cloud Shell or run from inside a Docker container.

[Download and install the latest release of the Azure CLI (64-bit)](https://aka.ms/installazurecliwindowsx64). When the installer asks if it can make changes to your computer, select the "Yes" box.

**<mark>Important:</mark>**

**<mark>After the installation is complete, you will need to close and reopen any active terminal window to use the Azure CLI.</mark>**

* Open the CMD terminal.
    
* Select the drop-down arrow to change the environment to `Azure Cloud Shell`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723500477829/8d6c4e26-265c-4ce4-8408-954107fe167d.png align="center")

* You will be prompted to sign in using a web browser. Follow the instructions to sign in.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723500669961/8d1d19df-44dd-4057-8c2d-bb9f4b691920.png align="center")

* Type "y" to save the connection string for future logins.
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723500876325/e4b6d6cd-e0cc-4b83-895f-77a7035fb71e.png align="center")
    
    ![A screenshot of a terminal window shows a session in Azure Cloud Shell. ](https://cdn.hashnode.com/res/hashnode/image/upload/v1723500917224/92b3af8e-30ee-427f-ab28-f3324f995717.png align="center")
    
    Use the following Bash commands to Deploy the ARM template in the terminal window
    

1. **Log in to Azure**:
    
    ```bash
    az login
    ```
    
2. **Create a Resource Group**:
    
    ```bash
    az group create --name MyResourceGroup --location eastus
    ```
    
    3. **Deploy the Template**:
        
        ```bash
        az deployment group create --resource-group MyResourceGroup --template-file azuredeploy.json --parameters vmName=myVM adminUsername=azureuser adminPassword=Pa$$w0rd!
        ```
        
        ## Step 4: Verifying the Deployment
        
        Once the deployment is complete, you can verify it by checking the Azure portal. Navigate to the resource group you created and ensure all resources are deployed correctly.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723510647366/3fddb959-0ab7-44c7-963b-67545dbebf22.png align="center")
        
        ## Conclusion
        
        Deploying Azure resources using ARM templates streamlines the process, ensuring consistency and reducing manual errors. With this guide, you can now create and deploy a simple VM using ARM templates. As you become more familiar, you can extend your templates to include more complex configurations and resources. Happy deploying!