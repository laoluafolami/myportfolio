---
title: "Creating Azure Virtual Network with 4 Subnets Using the Address Space 192.148.30.0/26"
datePublished: Fri Jul 12 2024 15:30:29 GMT+0000 (Coordinated Universal Time)
cuid: clzr0qroa000k08kz21uebs69
slug: creating-azure-virtual-network-with-4-subnets-using-the-address-space-19214830026
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723468662090/bde27504-ea19-4040-940f-fc9d139415fe.jpeg

---

**Azure Virtual Network (VNet)** is a fundamental service in Microsoft Azure that creates a private network environment within the Azure cloud. It functions similarly to a traditional network you might have on-premises, but with the added benefits of Azure's scalability, availability, and security features.

Here's a breakdown of key functionalities of an Azure VNet:

**Isolation and Security**: VNet isolates your Azure resources, such as virtual machines (VMs), from the public internet and other VNets. This isolation creates a secure environment for your applications to communicate with each other without worrying about unauthorized access.

**Subnet Creation**: VNets can be further segmented into subnets. Subnets act like sub-divisions within the VNet, allowing you to group related resources and define specific access controls for each subnet.

**IP Address Management**: VNets use a private IP address space (like the one you provided: 192.148.30.0/26) for resources within the network. This allows for private communication between resources without conflicting with public IP addresses.

**Connectivity Options**: VNets offer various options for connecting resources:

**Internet Access**: Subnets can be configured to allow resources controlled access to the internet through outbound rules in network security groups (NSGs).
VNet Peering: VNets can be peered together to enable communication between resources across different VNets within the same region.
VPN Gateway: VNets can connect to your on-premises network using a VPN gateway, creating a hybrid network environment.
Integration with Azure Services: VNets can integrate with various Azure services like Azure SQL Database or Azure Storage. By placing these services within a VNet, you can enforce private access only from authorized resources within the VNet.

## Benefits of using Azure Virtual Network:

**Improved Security**: Isolation and access control features enhance the security of your cloud resources.
Simplified Management: VNets provide a centralized way to manage and configure your network infrastructure in Azure.
Scalability: You can easily scale your VNet by adding or removing subnets as needed.

**Flexibility**: VNets offer various connectivity options to suit your specific needs.

In summary, Azure VNet is a critical component for building secure and scalable private networks within the Azure cloud environment. It provides a foundation for deploying and managing your Azure resources while ensuring their isolation and controlled access.

## Steps in Creating Azure Virtual Network with 4 Subnets.

**Step 1: Sign in to Azure Portal**

1. Open your web browser and navigate to the [Azure Portal](www.portal.azure.com).

2. Sign in with your Azure account credentials.

**Step 2: Navigate to Virtual Networks**

1. Click on **Create a resource**.

2. In the "Search the Marketplace" box, type Virtual Network and press Enter.

3. Click on Virtual Network in the search results.

![Creating a Resouce](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468646589/e3bb6ebb-0f14-4a4b-9102-4bc5c1910c90.png)

![Virtual Network](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468647960/d43f695e-0ec8-4316-9340-83cd48f843b6.png)

![Create](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468649336/f09d9c5b-9f48-4094-9713-d812dbf2dc52.png)

Click on the **Create** button.

**Step 3: Create a Virtual Network**

- 
In the "Basics" tab, fill in the following details:
**Subscription**: Select your subscription.
**Resource group**: Create a new resource group or select an existing one.
**Name**: Enter a name for your virtual network (e.g., _MyVNet_).
**Region**: Select the region where you want to create the virtual network.

- 
Click on Next: IP Addresses.

![Basic tab](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468650706/dc655c82-e4a2-4c9e-9a8e-7d2324d827a5.png)

**Step 4: Configure Address Space**

- 
In the "IP Addresses" tab, modify the existing address space to 192.148.30.0/26.


Click on **Add a subnet.**


![IP address](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468652006/0ee359f0-a251-46c6-87f1-c14234ba97b6.png)

**Step 5: Add Subnets**

Enter the following details:

1. 
**Subnet name:** Enter a name for the subnet (e.g., Subnet1).

2. 
**Subnet address range**: Enter the address range for the first subnet (e.g., 192.148.30.0/28).

- 
Click on Add.


![subnet1](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468653719/9a36ca82-03c9-463b-93ee-663b99b835d1.png)


![Image description](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468655160/37c205cb-63f4-4a81-96c1-c31e52b2f521.png)

- 
Repeat  1 & 2 above to add the remaining three subnets with the following details:


## Subnet2: 192.148.30.16/28

![subnet2](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468656553/997a4769-7335-4fa1-bdeb-df10e54d68e7.png)


## Subnet3: 192.148.30.32/28


![subnet3](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468657907/2d8a8b01-cf42-434f-b307-06c83ade303c.png)


## Subnet4: 192.148.30.48/28

![subnet4](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468659111/bd882e69-28bb-409b-8653-824fe7243970.png)


![Create](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468660461/e2189085-bd0b-406f-9731-1b595737353e.png)

**Step 6: Review and Create**

- 
Click on Review + create to review your configuration.

- 
After the validation passes, click on Create.

**Step 7: Verification**

- 
Once the deployment is complete, navigate to the Resource Group you selected earlier (**RG1**).

- 
Click on your Virtual Network (e.g., MyVNet).
Verify that the address space and subnets are correctly configured.








