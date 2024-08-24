---
title: "Practical IoT solution using Azure IoT Hub."
datePublished: Fri Jul 19 2024 06:37:50 GMT+0000 (Coordinated Universal Time)
cuid: clzr0qclq000i09jrel187nb4
slug: practical-iot-solution-using-azure-iot-hub
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723468642661/592d787e-1400-4046-8a0f-a809329ee1d8.jpeg

---

Microsoft Azure offers Azure IoT Hub, a robust managed service that serves as a single hub for managing and connecting Internet of Things (IoT) devices. Let us examine the specifics:

**Objective and Usability:**
Central Hub: The foundation of all IoT applications developed on the Azure platform is Azure IoT Hub. It makes it easier for cloud services and Internet of Things devices to communicate seamlessly.
Secure and consistent connectivity is guaranteed between your IoT application and the devices it is linked to.

- 
**Scalability**: An IoT Hub instance may be linked to millions of devices.

- 
**Device Management**: The IoT Hub has tools for managing, authenticating, and provisioning devices.

**Important characteristics:**

- 
**Device-to-Cloud Telemetry**: Gather information from gadgets to comprehend their condition and actions.

- 
**Cloud-to-Device Messages**: Notifications and orders can be sent to linked devices from the cloud.

- 
**Security and Authentication**: To improve security, authenticate every device separately.

- 
**Automate the registration and provisioning of devices**.

- 
**Over-the-Air Updates**: Update firmware and software on devices to keep them current.

- 
**Integration with Azure Services**: You can effortlessly include Event Grid, Azure Functions, and other Azure services with ease.

- 
**IoT Edge Integration**: Use Azure IoT Edge to expand your solution from the cloud to the edge.

## **Use Cases:**

- 
**Smart Cities**: Keep an eye on and control traffic signals, trash cans, lamps, etc.

- 
**Industrial IoT**: Monitor the condition of machinery, enhance productivity, and raise security.

- 
**Healthcare**: Keep an eye on hospital facilities, medical equipment, and patient vitals.

- 
**Agriculture**: Gather information with sensors in cattle, greenhouses, and fields.

- 
**Retail**: Track assets, keep an eye on inventories, and improve customer service.

## Practical steps using a mobile device (Samsung phone).

- 
Set Up Azure IoT Hub.

- 
Register a Simulated Device (Samsung phone).

- 
Simulate the Device 

- 
Azure Blob Storage Integration.

## Step 1: Set Up Azure IoT Hub

- 
Log in to your [Azure](www.portal.azure.com) account.

- 
Search for “IoT Hub” and click “+ Add.”

- 
_Configure the settings below:_

_Name_: Choose a unique name for your IoT Hub.

_Pricing Tier_: Select the appropriate tier based on your requirements.

_Resource Group_: Create a new one or use an existing group.

_Region_: Choose a region close to your devices.

- 
Click on **Review + Create**

![IoT Hub](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468585828/b2e37f59-c95a-42a8-b5fc-de856d3d803a.png)


![IoT Hub](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468587271/7129ae55-c7d8-493b-8dff-6ff408023015.png)
![Resource](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468588510/073d98aa-4c50-4f1b-b149-e6a430adb9c4.png)

## Step 2: Register a Simulated Device.

_Create a Simulated Device:_

- 
From your IoT Hub overview page:

Click **Device** from the _Device management blade._

- 
Select **+ Add device.**


![Device Add](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468590090/9abf42f8-75ac-4439-86a9-8cc8782e4250.png)

- 
Provide the **Device ID**

- 
Choose an authentication type (e.g., _symmetric key_).

- Leave the default values of the other fields and select **Save**.

![Device](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468591538/e451e8d6-6aa7-4fa6-ad2d-2120e932f9bd.png)

- 
Go to the _Device Overview_ page and click the newly created device (_Samsungphone_).


![Device](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468592800/a0be213b-de58-49ae-8bb4-491ab24daf4c.png)

- 
On your device (The smart phone in this case the Samsung phone), go to _Playstore _ and download the app called **IoT PnP**

- On the landing page, click on _Scan QR code_  as indicated below.

![QR code](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468593912/dc441784-c3ed-4536-a4c3-d921d82d0eb8.png)

- Click on _Manually connect_.


![connect](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468595611/06f0c9b6-1444-4f22-8eb8-68e0a703e758.png)

- 
Select the _IoT Hub device connection string_ radio button.


![Connection string](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468597249/9322fe00-6466-4aab-8417-a0ac6c7d2fd8.png)

- 
Paste the **Primary Connection String** in the _IoT Hub device connection string field_  and click the _Connect_ button.



![Connect string](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468598957/d9ba8724-6aaa-447f-9136-425bb4a16fa4.png)

- 
The telemetry data of the phone is displayed.


![Telemetry details](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468600374/07959102-a533-4fc3-9c21-bb5a32cd5215.png)


## Azure Blob Storage Integration 
- 
Navigate to the IoT device overview page and select **Message routing** from the _Hub settings_ blade.


![Message Route](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468602086/764e6ca2-874f-488d-adc0-da3283ac8c33.png)

Select **+ Add** to add a route.


![+ Add](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468603459/afa44be4-8fb5-447f-b4d1-db126528b28c.png)

- Select **Storage** as the _Endpoint type_, provide the _Endpoint name_ and select the **Jason** as the _encoding type_.

- 
Click on the **Pick a container** button to begin creating a storage account.

![Endpoint](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468605117/3d6a7fc8-f1f2-49b5-a1fe-1112ba4c8da9.png)

- 
Click the **+ Storage account** option to create a storage account.

![Storage](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468606418/ae33013d-5c59-493f-bb77-225c0ceb77f8.png)

- 
Provide the Storage details as indicated in the screenshot below and click the _Ok button_:


![Storage](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468607534/b8a7905a-98d1-4ce9-8ec9-aff5bb2003d4.png)

- 
Select the created storage account (_phonestorage_). 

![Storage](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468609120/5c6b7217-4463-4886-a87d-e03b32221fc5.png)

- 
Create a Container.
![Container](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468610219/a698d0fb-46d9-4ee5-99f1-ef66dcb58799.png)


![storage](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468611873/236a2d85-8dfd-4113-bc38-9d32a51f1456.png)

- 
Click on _Create_ to provision the container (_phonefiles_) .


![Container](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468613437/46a10457-5baf-46fb-af2b-1a694a565be0.png)

- 
Select the container created.


![Container](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468614496/9032f6c7-1242-4ce1-9840-b33132e48d0d.png)

- 
Click the _Create + next button_ to proceed.


![Proceed](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468615652/0985240f-5f27-4b3c-9240-da72798fdda1.png)

- 
Enter a route name and select a _Device Telemetry message_ in the Data source drop-down and click **Test** to test the route.


![Route](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468617067/18af24d4-eb25-4b7d-ba7a-27935fe12cc5.png)

- 
Click the _Create + add enrichment button.


![enrichment](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468618234/1b58e5f9-4adf-4eab-ae6d-4b9e0d842b08.png)

- 
Click the _Add button_.


![rtt](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468619448/b833f327-c9d0-4a6f-b64b-e7f01d05b97e.png)

- Navigate to the created IoT hub212 and select _File upload_ from the **Hub settings** blade.


![fileupload](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468620764/0f17f34f-9369-4106-86a2-2341b9c2003d.png)

- 
Select _Azure storage container_.

![Storage container](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468621922/51ecdb7b-b42b-44e1-b962-fd61c773f93c.png)

- 
Select the created container (_phonefiles_).

![Container](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468623068/f4c4dc4c-b57d-4998-b638-857d1fcacaf5.png)

- 
Turn on _file notification settings_ then click save.


![Image](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468624471/9b381cdd-3d56-4f3c-8084-368acc23529d.png)

- 
From your mobile phone, click on _Image upload_.
 
![Image upload](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468625772/a35cdb71-1bd2-4421-8861-cbacd4701ec7.png)


![Image upload](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468627472/fd70c6ff-8238-483a-b687-496906670318.png)

- 
Upload an image from your phone.


![Image upload](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468629121/4643b9f6-6bc0-4c0b-9826-20021a7de83e.png)

- 
Navigate to your Blob Storage to view the uploaded file.


![storage folder](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468630695/89df75c0-c92e-495a-befe-522f847d5d95.png)

The uploaded files.


![Files](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468631969/978d201e-b51b-43a1-98bb-1e45e8f49669.png)

## Viewing the telemetry data using Visual studio code.

Navigate to the storage folder and download the Json files and view them in Visual studio code editor.


![Json files](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468633468/4d8fca9d-c591-4246-a9cc-ee618bdb563c.png)


![Image description](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468634945/de9a0b22-e5b0-45ae-b3e4-dd231f784106.png)

- 
For Bi-directional data, from your mobile phone, click on the Properties tab from the IoT plug n Play app.


![properties](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468636802/77fd048c-7198-4cac-8c0c-c1b48fde4dba.png)

- 
Click on the _Editable property_ tile, edit it with any word or sentence and click on _Send_.


![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468638560/10ba052b-9e7b-46c6-940e-0ead34d4487e.png)

- 
Navigate to the IoT hub and select the created device (_Samsungphone_) .


![device](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468639706/b85bb172-cd87-4849-89ab-984314cdae65.png)

- 
Click on **device twin**.

- 
The edited string now appears in line 37 of the Json code. 


![edited](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468641061/0d53b942-a938-41e5-a939-bcae8e451e29.png)

This simulation demonstrated the seamless integration between our device and Azure IoT Hub. Here are the key takeaways:
 
**Data Persistence in Azure Blob Storage:**

- 
Our device successfully saved telemetry data to Azure Blob Storage.

- 
This demonstrates the reliability and scalability of our chosen solution.

**Telemetry Monitoring:**

- 
We monitored the telemetry data from our mobile device, gaining valuable insights, and archived logs for auditing and troubleshooting.

- 
Real-time monitoring allows us to make informed decisions promptly.

**Exploring Further Use Cases:**

- 
Beyond this simulation, there are numerous other scenarios we can explore:
Image Storage: Store images captured by our devices.

- 
Streaming Data: Process real-time streams from sensors.

- 
Data Archiving: Long-term storage for compliance or historical analysis.

_Kindly comment, like and share._




















































































































