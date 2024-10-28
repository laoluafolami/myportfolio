---
title: "Simple Steps to Launch a Website with Apache2 on AWS EC2"
seoTitle: "Launch Website on AWS EC2 with Apache2"
seoDescription: "Website on AWS EC2 with Apache2"
datePublished: Mon Oct 28 2024 14:23:06 GMT+0000 (Coordinated Universal Time)
cuid: cm2t3zfsw000209ms28qagg0n
slug: simple-steps-to-launch-a-website-with-apache2-on-aws-ec2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1730125048161/e9871e97-7b24-4652-b51c-cc6593b7a2dc.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1730125217835/ed094074-6e8b-4b56-96ee-29f66f505bd0.png
tags: aws, apache, aws-ec2

---

Are you looking to host your first website and want to learn how to do it on AWS? You’re in the right place! In this guide, I’ll show you how to create an Amazon Web Services (AWS) EC2 instance, install an Apache2 web server, and host your website on it—all with simple, step-by-step instructions. Let’s dive right in!

## **What is AWS EC2?**

AWS EC2 (Elastic Compute Cloud) is a cloud-based virtual server that allows you to run applications or host websites. You don’t need to worry about hardware, and you only pay for the resources you use. Perfect for hosting your website!

## **Prerequisites**

Before we begin, you’ll need:

* An AWS account (sign up at [aws.amazon.com](https://aws.amazon.com/)).
    
* A basic understanding of how to use a terminal (for running commands).
    

### **Step 1: Launch an AWS EC2 Instance**

First, we need to launch our virtual server, known as an EC2 instance.

1. **Log into AWS**:
    
    * Head to the AWS Management Console.
        
    * Search for **EC2** and click on it to go to the EC2 dashboard.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729428299828/9752229b-a978-4bbf-82eb-0c99d76362fe.png align="center")
    
2. **Launch a New EC2 Instance**:
    
    * Click **Launch Instances**.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729428655064/25a77ceb-333a-463d-a401-a5224575325a.png align="center")
    
    * Give your instance a name, such as "MyFirstWebServer".
        
3. **Choose an Amazon Machine Image (AMI)**:
    
    * Select **Ububtu AMI** (this is free-tier eligible and perfect for beginners).
        
    * Click **Select**.
        
4. **Choose an Instance Type**:
    
    * The default **t3.micro** is sufficient for basic web hosting, and it’s free-tier eligible.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729428946826/e1afb26e-44c6-4198-99f0-475abd3e0f61.png align="center")
        
    * Scroll Down**: Configure Instance Details**.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729429310298/78fbaff5-f589-4879-a9a1-0357da228c9f.png align="center")
        
5. Select **Create a New Key Pair**, give it a name, and download the `.pem` file (this will allow you to SSH into your instance). Keep it safe!
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729429464465/602bd06b-443c-4ddb-bc7c-4f363c5abbac.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729429599184/a8601628-507b-4fb8-8d35-cb43edb7ef0f.png align="center")
    
6. **Set Up a Security Group**:
    
    * A security group acts as a virtual firewall for your instance.
        
    * Create a new security group with the following rules:
        
        * **SSH** (Port 22) to connect to your server.
            
        * **HTTP** (Port 80) to serve your website.
            
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729429782457/211c3f43-5435-4def-9e40-ae0d250cac75.png align="center")
    
7. **Add Storage**:
    
    * The default 8GB of storage is more than enough for a small website. Click **Next: Add Tags**.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729429843079/b13295a1-1545-4d78-97ab-ee0e49dd59e9.png align="center")
    
8. Click **Launch instance**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729429960527/cb7c920a-2717-48be-9a1c-755e82c260a9.png align="center")
    
9. **View Your Instance**:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729430134389/b00ad00c-9187-4bb4-a33c-7c29e2c90884.png align="center")
    
10. * Copy the **Public IPv4 address**—this is your website’s public address for now.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729430294274/da87141f-96a9-46bc-be32-ec07d32becd6.png align="center")
    
    ### **Step 2: Connect to Your EC2 Instance**
    
    Now that your instance is up and running, let’s connect to it and set up the web server.
    
    * **Open a Terminal (or PowerShell on Windows)**:
        
        * Navigate to the folder where your `.pem` key file is stored.
            
    * **Connect via SSH**:
        
        * Run this command (replace `<your-key-file>` with your `.pem` file name and `<ec2-public-ip>` with the EC2 instance public IP address):
            
        * ```bash
            chmod 400 <your-key-file>.pem
            ssh -i "<your-key-file>.pem" ubuntu@<ec2-public-ip>
            ```
            
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729434116166/579613fc-2dd4-4fa4-8bba-065debd1ed39.png align="center")
        
        If prompted, type `yes` to connect.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729434388715/6a09d493-7b9b-45be-bd9e-6e8dabdd6478.png align="center")
        
        ### **Step 3: Install Apache2 Web Server**
        
        Now, let's set up the Apache2 web server that will host your website.
        
        1. **Update Your Package Manager**:
            
            * After connecting to your EC2 instance, run this command to ensure your system is up to date:
                
    
    ```bash
    sudo apt update
    ```
    

* **Install Apache2**:
    
    ```bash
    sudo apt install apache2 -y
    ```
    
* **Start Apache2 server**
    
    ```bash
    sudo systemctl start apache2
    ```
    
* **Enable Apache2 to Start on Boot**:
    
    This ensures Apache starts automatically if your instance reboots
    
    ```bash
    sudo systemctl enable apache2
    ```
    
    * **Verify Apache2 is Running**:
        
        Open your browser and visit:
        
    
    ```xml
    http://<ec2-public-ip>
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729436835294/6b27e1f4-bae8-4efe-a7a4-0a193ae44e16.png align="center")
    
    ### **Step 4: Host Your Website on Apache2**
    
    My website files are stored in my Github repository ([https://github.com/laoluafolami/kids](https://github.com/laoluafolami/kids)). You can clone this site or simply use your own source files.
    
* Now that Apache is running, let’s replace the default page with your website.
    
    1. **Navigate to the Web Root Directory**:
        
        * Run this command to go to the folder where your website files will be stored:
            
        
        ```bash
        cd /var/www/html
        ```
        

Clone the website files from my repository:

```bash
sudo git clone https://github.com/laoluafolami/kids.git
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729519579943/e9bd99b7-ecbf-4b7a-a6fb-16c096e59faa.png align="center")

Navigate to the folder where you have your cloned repository.

```bash
cd kids
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729519704783/f89adf27-8755-44b3-a9ee-730d51e26409.png align="center")

* Move the files in your cloned repository to the default Apache2 web root folder (/var/www/html).
    
    ```bash
    sudo mv * /var/www/html
    ```
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729520225391/5197ce97-56d9-4e1e-a5bb-5374092cb698.png align="center")
    
    **Test Your Website**:
    
    Go to your browser and visit:
    
    http://&lt;ec2-public-ip&gt;
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729520698794/53993136-b0e5-4938-9d81-f7b4ea350f09.png align="center")
    
    http://13.49.241.203
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729520786771/e4bc01e8-9e84-4285-965b-27dc493084c6.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729520891053/275ddea9-4f4a-4e42-91cc-d9e4a7d8f91d.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729520912449/8d3aa734-7779-4122-b0a0-c8ac2a5524a5.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1729520938449/1037ffaa-eb2a-442a-9a51-6fec5ebcbb99.png align="center")
    
    ### **Conclusion**
    
    Congratulations! You’ve successfully set up an EC2 instance, installed Apache2, and hosted your first website. This is a great first step into the world of cloud computing and web hosting