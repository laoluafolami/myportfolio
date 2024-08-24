---
title: "Hosting a Static Website Using Microsoft Azure Blob Storage"
datePublished: Thu Jul 04 2024 10:17:18 GMT+0000 (Coordinated Universal Time)
cuid: clzr0rb1t00020ajv75lx089f
slug: hosting-a-static-website-using-microsoft-azure-blob-storage
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723468686467/febdcd38-98ec-485f-804f-f1742406b12e.jpeg

---

Microsoft's cloud storage solution for contemporary data storage scenarios is the Azure Storage platform. For a range of cloud-based data items, Azure Storage provides highly accessible, massively scalable, robust, and secure storage. Anywhere in the globe may access Azure Storage data objects using HTTP or HTTPS.
All kinds of data are stored in Azure storage. Its primary purpose is to provide easy access to storage for both structured and unstructured data. Your static website may be quickly uploaded to Microsoft Azure, where you can establish access control and share the URL with anybody to see your website.

In this article I will demonstrate how to setup a static website using the Azure portal. Let's dive in.

**Log in to the Azure Portal and create an Azure storage account.**
Click on the [Azure portal](www.portal.azure.com). 

**Create an Azure storage account**.

- 
Search for storage accounts and click on it.


![Storage accounts](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468666407/85033557-ff9f-412f-bff5-09abcd9d82a1.png)


**Create a Storage account**

![Create a storage account](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468667861/e17257b3-0d8a-4075-b95a-2692015f939e.png)

**Create a Resource Group**.
Create or select an existing Resource Group. 
Give your storage account a unique name eg _webstore212_.
Click on _Review + create_.


![Create a RG](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468669069/7ca67550-eb39-4153-8849-719165493e7a.png)

After the deployment is completed, click the _Go to resource_ button.

![Goto Resource](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468670370/6bf9168e-6a4d-487e-9abf-d6b7b7811b9c.png)

**From the Storage overview page**.

- Scroll to the _Data management _ blade and select _Static website_.


![Static website](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468671741/2a9e97c3-669e-4042-9ec1-919f780a3801.png)

- 
Enable the static websites on the blob service to host a static content.

- 
Enter the _index document name_ and the _Error document path_.

- 
Click _Save_.


![Static site](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468673066/6d046bbe-e8dd-4ed7-b5fa-27e9a5bc5c48.png)

- From the _Data storage_ blade, select _Containers._
(Note that a new container has been created named _web_.

- Click the _web_ container.


![data storage](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468674226/e0924e4b-b969-43f2-bfbd-4770e47cd744.png)

- In the web storage tier, upload your website files by clicking on the _upload_ button.


![web](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468675802/0cb8680c-66a8-49f3-b357-2a7a3c7dd44a.png)

- Browse to where you have your website file or Drag and drop your website files.


![Upload files](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468677276/ef1fcd65-70b5-4571-9a7e-917beb23c172.png)


![files](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468678546/4aae26ce-5b69-4d7b-a403-a39cf24969a8.png)


- Click on _Upload_ to complete the process.


![Upload files](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468679580/6b340d3a-ef22-4552-9306-53fd7dd8c01d.png)

**A view of the uploaded files**.


![Uploaded files](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468680663/a33f647d-6da7-42a2-9b13-cdd58e3226eb.png)

- 
Navigate to the storage account and under the _Data management_ blade, select _Static website_ 

- Look for _Primary endpoint_ to the right of the page and copy the endpoint URL.


![endpoint url](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468682010/5f49b9b1-1b9b-402b-958b-407ba84fcd2d.png)

- Paste the URL in a browser to access the webpage. 


![Web](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468683476/c894e59f-7327-43dd-b2a3-181d49351cf3.png)

- 
The displayed website.


![Image description](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468685107/668c850d-73a2-4882-bef4-cdc1998c1895.png)























 

























