---
title: "Learn How to Deploy a Virtual Machine in Azure with Terraform: Step-by-Step Tutorial"
seoTitle: "Learn How to Deploy a Virtual Machine in Azure with Terraform"
seoDescription: "Terarform"
datePublished: Fri Oct 04 2024 12:35:00 GMT+0000 (Coordinated Universal Time)
cuid: cm1upjzhb001v09k177nc06du
slug: learn-how-to-deploy-a-virtual-machine-in-azure-with-terraform-step-by-step-tutorial
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1728045185618/20ee4d8f-2ec3-400b-a664-04981e5ada01.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1728045246634/ae29bf32-efbb-45b6-bc8e-4edb679e3c4a.png
tags: azure, terraform

---

### **What is Terraform?**

Terraform is an open-source Infrastructure-as-Code (IaC) tool developed by HashiCorp. It allows you to define and provision infrastructure using a high-level configuration language. Terraform enables users to automate the setup, configuration, and management of cloud resources like virtual machines, networks, storage, and more.

Infrastructure as Code (IaC) tools allow you to manage infrastructure with configuration files rather than through a graphical user interface. IaC allows you to build, change, and manage your infrastructure in a safe, consistent, and repeatable way by defining resource configurations that you can version, reuse, and share.

Terraform is HashiCorp's infrastructure as code tool. It lets you define resources and infrastructure in human-readable, declarative configuration files, and manages your infrastructure's lifecycle. Using Terraform has several advantages over manually managing your infrastructure:

* Terraform can manage infrastructure on multiple cloud platforms.
    
* The human-readable configuration language helps you write infrastructure code quickly.
    
* Terraform's state allows you to track resource changes throughout your deployments.
    

You can commit your configurations to version control to safely collaborate on infrastructure.

**<mark>Using Terraform for infrastructure deployment:</mark>**  
  
**Scope:** Identify what is required for your project.  
  
**Author**: Compose the infrastructure's configuration.  
  
**Initialise**: Install the plugins that will be managed by Terraform.  
  
**Plan:** Preview the changes Terraform will make to match your configuration.  
  
**Apply:** Make the planned changes.

## **Step 1: Prerequisites**

Before you begin, you need the following:

* **Azure Account**: If you don’t have one, create it [here](https://azure.microsoft.com/en-us/free/).
    
* **Terraform Installed**: Install Terraform by following the instructions on the Terraform website.
    
* **Azure CLI Installed**: Download and install Azure CLI from [here](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli).
    
* **Text Editor**: Any text editor, such as Visual Studio Code, Sublime, or Notepad++.
    

## **Step 2: Authenticate to Azure**

After installing the Azure CLI, you need to log in to your Azure account. Run the following command in your terminal or command prompt:

```bash
az login
```

A browser window will open where you can enter your credentials. Once you are authenticated, you can close the browser.

## **Step 3: Create a Directory for Your Terraform Files**

You will write all your Terraform code inside a directory on your local PC. Let's create one and navigate into it (*I created the “azure-vm-terraform” folder inside a “Project” folder in the “Documents” folder*):

```bash
mkdir azure-vm-terraform
cd azure-vm-terraform
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728036974074/e236c120-5a4b-448a-9358-10a20787fefa.png align="center")

## **Step 4: Create a Terraform Configuration File**

In the directory you created, you need to create a Terraform configuration file. Let’s call it [`providers.tf`](http://main.tf). Open your text editor and create the file with the following content:

```yaml
terraform {
  required_version = ">=1.0"

  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~>3.0"
    }
    random = {
      source  = "hashicorp/random"
      version = "~>3.0"
    }
  }
}
provider "azurerm" {
  features {}
}
```

Next, you create another file named `main.tf`, with the following content:

```yaml
resource "azurerm_resource_group" "example" {
  name     = "aflameRG"
  location = "East US"
}

resource "azurerm_virtual_network" "example" {
  name                = "aflame-VNET"
  address_space       = ["10.0.0.0/16"]
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name
}

resource "azurerm_subnet" "example" {
  name                 = "aflame-Subnet"
  resource_group_name  = azurerm_resource_group.example.name
  virtual_network_name = azurerm_virtual_network.example.name
  address_prefixes    = ["10.0.1.0/24"]
}

resource "azurerm_network_interface" "example" {
  name                = "aflame-NIC"
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name

  ip_configuration {
    name                          = "internal"
    subnet_id                     = azurerm_subnet.example.id
    private_ip_address_allocation = "Dynamic"
  }
}

resource "azurerm_virtual_machine" "example" {
  name                  = "aflame-VM"
  location              = azurerm_resource_group.example.location
  resource_group_name   = azurerm_resource_group.example.name
  network_interface_ids = [azurerm_network_interface.example.id]
  vm_size               = "Standard_DS1_v2"

  storage_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }

  storage_os_disk {
    name              = "aflameOSDisk"
    caching           = "ReadWrite"
    create_option     = "FromImage"
    managed_disk_type = "Standard_LRS"
  }

  os_profile {
    computer_name  = "Aflame-PC"
    admin_username = "adminuser"
    admin_password = "Password1234!"
  }

  os_profile_linux_config {
    disable_password_authentication = false
  }
}
```

### **What does this file do?**

The `.tf` extension in `main.tf` and `providers.tf` is to denote that it is a terraform file.

* **Provider**: Specifies that you’re using Azure as your cloud provider.
    
* **Resource Group**: Creates a new Azure resource group to hold all your resources.
    
* **Virtual Network**: Creates a virtual network.
    
* **Subnet**: Creates a subnet inside the virtual network.
    
* **Public IP Address**: Creates a public IP address for the VM.
    
* **Network Interface**: Creates a network interface card (NIC) for the VM.
    
* **Virtual Machine**: Deploys a Linux VM (Ubuntu 18.04) in the Azure region `East US`.
    

## Step 5: Initialize Terraform

Before Terraform can manage your infrastructure, you need to initialize it by running the following command. This command downloads the Azure provider required to manage your Azure resources.

```bash
terraform init
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728039282740/c7ef7940-19ad-41f6-aebd-40c5de05cf85.png align="center")

You can also use `terraform init -upgrade`. The `-upgrade` parameter upgrades the necessary provider plugins to the newest version that complies with the configuration's version constraints.

## **Create a Terraform execution plan**

Run `terraform plan` to create an execution plan.

```bash
terraform plan -out main.tfplan
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728039924494/fcedc046-1d8c-4a69-a139-6ae93a745931.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728039985035/48a9f57e-b364-4c64-b64e-424afb2c2a18.png align="center")

* The `terraform plan` command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources.
    
* The optional `-out` parameter allows you to specify an output file for the plan. Using the `-out` parameter ensures that the plan you reviewed is exactly what is applied.
    

## **Step 6: Apply the Terraform Configuration**

To create the resources defined in your file [`main.tf`](http://main.tf), run the following command:

```bash
terraform apply
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728040261795/40ccc78c-8d84-45b4-b858-16a0d7b071c2.png align="center")

Terraform will show you the resources that will be created. Type `yes` to confirm and start the deployment.

Cost information isn't presented during the virtual machine creation process for Terraform like it is for the Azure portal.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728040437146/77293826-ed91-438e-a4ac-9f155514acb8.png align="center")

## [**Step 7: Ve**](https://learn.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-portal)**rify the Virtual Machine in Azure**

Once Terraform completes, your VM will be created in Azure. You can log in to the Azure Portal here and verify that the virtual machine, resource group, and other resources have been deployed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728040649102/8c504a0a-6440-4585-90ca-da10aba0f1d5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728040874024/15b515ca-9f86-4718-aa77-ac3c2ef08e04.png align="center")

## **Step 8: Access Your Virtual Machine**

Now that your VM is running, you can access it via SSH. Run the following command:

```bash
ssh azureuser@<your_public_ip>
```

Replace `<your_public_ip>` with the public IP address assigned to your VM, which you can find in the Azure portal or in the Terraform output after the `apply` step.

## **Step 9: Destroy the Resources (Optional)**

When you're done experimenting, you can clean up the resources by running:

```bash
terraform destroy
```

This will delete all the resources that Terraform created in Azure.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728041072363/0624fdba-bdd1-4a91-92fd-becb8f2df4d1.png align="center")

## **Conclusion**

You’ve successfully created an Azure Virtual Machine using Terraform! This is a basic example, but Terraform can be used to manage complex infrastructure in a scalable and repeatable way.

---

Feel free to ask if you need further clarification on any part of the guide.

Like and share.