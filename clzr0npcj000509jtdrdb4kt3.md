---
title: "Deploying a web app with CI/CD pipeline on Azure App Service."
seoTitle: "Deploying a web app with CI/CD pipeline on Azure App Service."
seoDescription: "Webapp"
datePublished: Sat Aug 10 2024 00:09:07 GMT+0000 (Coordinated Universal Time)
cuid: clzr0npcj000509jtdrdb4kt3
slug: deploying-a-web-app-with-cicd-pipeline-on-azure-app-service
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724513226393/914a8176-c648-4f1a-a44b-16fa6193f979.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1724513252161/a57328d4-a544-420c-a349-feecfb588cd3.png
tags: azure-webapp, cicd-pipeline, appservices

---

## Azure App Service

Azure App Service is a fully managed platform-as-a-service (PaaS) offering by Microsoft Azure that enables developers to build, deploy, and scale web applications, mobile backends, and RESTful APIs quickly. It supports various programming languages and frameworks, including .NET, Node.js, Java, Python, PHP, and Ruby, allowing developers to work in their preferred environment.

**Key Features:**

**Managed Hosting:** Azure App Service takes care of infrastructure management, so you don’t need to worry about server maintenance, patching, or scaling.

**Automatic Scaling:** It supports auto-scaling, allowing your application to handle varying loads by automatically scaling out or in based on traffic.

**Continuous Deployment and Integration:** It integrates seamlessly with GitHub, Azure DevOps, and other CI/CD tools, enabling automated deployments.

**Built-in Monitoring and Diagnostics:** Application Insights and Azure Monitor provide deep insights into the performance and health of your applications.

**Security:** Supports custom domain SSL, authentication with Azure Active Directory, and compliance with security standards like ISO and SOC.

## Azure App Service Plan.

An Azure App Service Plan defines the region, resource allocation (CPU, memory, etc.), and pricing tier for the apps hosted in Azure App Service. Essentially, it represents the underlying infrastructure that supports your web app.

**Key Components:**

**Region:** The geographical location where your App Service Plan’s resources are hosted.

**Pricing Tiers:** There are multiple tiers ranging from Free to Premium, each offering different levels of compute resources, scaling options, and features.

**Free/Shared:** Basic tiers for development and testing with limited features.

**Basic:** Suitable for low-traffic production sites with up to three instances.

**Standard:** Includes autoscaling, traffic manager, and more advanced features.

**Premium:** For high-traffic, mission-critical apps needing higher performance, more instances, and additional features like VNET integration.

**Resource Allocation:** The plan determines how much compute power, memory, and storage your apps can use.

## Key Benefits:

**Cost Management:** By adjusting the tier of your App Service Plan, you can optimize costs according to your application’s needs.

**Multiple Apps:** You can host multiple apps on the same App Service Plan, sharing the allocated resources, which helps in efficient resource utilization.

**Flexible Scaling:** Depending on the tier, you can scale out (add more instances) or scale up (move to a more powerful tier) based on the demands of your application.

Together, Azure App Service and App Service Plans provide a robust, scalable, and cost-effective solution for hosting web applications and APIs on the cloud.

## Use Cases and Scenarios.

Azure App Service and App Service Plan are versatile tools that cater to a wide range of scenarios:

**Web Hosting:** Azure App Service is ideal for hosting websites and web applications, whether they're simple static sites or complex, enterprise-grade applications. Its support for multiple languages and frameworks makes it a go-to solution for developers working in diverse environments.

**API Hosting:** Azure App Service is also well-suited for hosting RESTful APIs. The platform's built-in authentication and authorization capabilities, along with seamless integration with Azure API Management, make it easy to manage and secure APIs.

**Mobile Backend:** App Service can serve as the backend for mobile applications, offering features like offline sync, push notifications, and authentication services. This makes it a robust solution for mobile app developers who need a reliable and scalable backend.

**Continuous Deployment:** For teams practicing DevOps, Azure App Service supports continuous integration and deployment, allowing code changes to be automatically deployed to production. This reduces manual intervention and helps maintain a continuous delivery pipeline.

**Multi-Tenant Applications:** Azure App Service can host multiple web apps within a single App Service Plan. This is particularly useful for multi-tenant applications where different clients or customers share the same infrastructure while maintaining isolation.

## STEPS:

**1\. Create an Azure App Service Plan**

Log in to the [Azure Portal](www.portal.azure.com).

Click on `Create a resource` and search for `App Service Plan`.

Click `Create` and provide the following details:

**Subscription:** Choose your Azure subscription.

**Resource Group:** Select an existing resource group or create a new one.

**Name:** Provide a name for your App Service Plan.

**Region:** Choose the region that is closest to your users.

**Pricing tier:** Choose the pricing tier based on your app's requirements (the free tier is suitable for small applications). Click `Review + Create` and then `Create` to provision the App Service Plan.

![Azure app service plan](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468494515/5502a063-07aa-4478-87ee-15af5a38828e.png align="left")

![create](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468495782/ff228431-e54f-46dc-98fc-abbc3e3af855.png align="left")

**2\. Create an Azure App Service**

Navigate to "App Services" and click "Create".

![app services](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468497386/a9fea0ad-1000-42d5-bd02-3b14fac4d4e3.png align="left")

![app services](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468498660/b3490453-6635-4c89-8d47-298c348bb660.png align="left")

Provide the necessary details: **Subscription:** Select the subscription you used in the previous step.

**Resource Group:** Choose the resource group where your App Service Plan is located.

**Name:** Give a unique name to your web app.

**Publish:** Choose `Code`.

**Runtime stack:** Select the language stack (e.g., Node.js, .NET, Python).

**Region:** Choose the same region as your App Service Plan.

**App Service Plan:** Select the App Service Plan you created earlier.

Click `Review + Create` and then `Create` to deploy your App Service.

![webapp](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468500211/bbe02468-6c24-475a-81df-759b0bb1136f.png align="left")

![webapp](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468501857/18611328-a046-4358-a06f-ecc88c376568.png align="left")

![Create](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468503340/7082c592-3230-4434-98a7-f695e692d569.png align="left")

Click `Go to resource`.

![goto](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468504745/90eb9e9a-1477-4269-b081-8a117a7d149f.png align="left")

## 3\. Prepare Your Web Application.

Log in to your Github account and create a new repository.

![Github](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468505940/193d6728-83df-4a6f-ba3d-6356d0199f50.png align="left")

![New repo](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468507598/e4c61f27-89f7-4f4d-ba49-3a2390996a0f.png align="left")

![New repo](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468509282/47e77963-4dee-45a3-802d-29fac14de2e6.png align="left")

![wepapp repo](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468510377/b45d13a4-0667-45b5-b5e2-a66323daacfb.png align="left")

Click on `Code` and copy the web URL.

Open Visual Studio code and select the `Terminal` =&gt; `New terminal`

Change the terminal to `Bash`

![VScode](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468511960/08645d5b-51f6-4da5-b3e9-35a848fa1a82.png align="left")

Create a folder which will contain all the files for your site and then clone the repository you created in Github.

![Git repo](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468513141/7fc7620b-e888-4ad8-9a47-a059ad970961.png align="left")

![git clone](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468514255/5f424c08-d5af-459b-ae3c-59953e180026.png align="left")

In Visual Studio code, navigate to the folder created and create a new file called index.php and add a simple code below.

```bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple PHP Website</title>
</head>
<body>
    <header>
        <h1>Welcome to My Simple PHP Website</h1>
        <nav>
            <ul>
                <li><a href="index.php">Home</a></li>
                <li><a href="about.php">About</a></li>
                <li><a href="contact.php">Contact</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <h2>Home Page</h2>
        <p>This is the home page of my simple PHP website.</p>
    </main>

    <footer>
        <p>&copy; 2024 Simple PHP Website</p>
    </footer>
</body>
</html>
```

![VScode](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468515699/3a255fa6-47b1-4438-a115-ea4b04ec3155.png align="left")

Use the commands `Git add .`, `git commit` and `git push` to add the newly created file *index.php* to Github.

![git push](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468516991/5f9aa2bc-871e-4681-92b2-39604b1f1e13.png align="left")

## 4\. Configure GitHub Actions for CI/CD

GitHub Actions is a powerful tool to automate your CI/CD process directly from your GitHub repository.

In the Azure Portal, navigate to your App Service.

Select `Deployment Center` in the *Deployment blade*.

Select `Github` as the *Source*.

![Image description](https://cdn.hashnode.com/res/hashnode/image/upload/v1723468518700/1e8e1e99-5f04-459a-98f3-f5ce28dd46bd.png align="left")