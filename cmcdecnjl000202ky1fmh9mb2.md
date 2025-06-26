---
title: "Dockerise Your React.js Portfolio Website."
seoTitle: "docker"
seoDescription: "docker"
datePublished: Tue Jun 24 2025 23:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cmcdecnjl000202ky1fmh9mb2
slug: dockerise-your-reactjs-portfolio-website
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1750942909943/0c6f62f2-feee-43ca-956f-0b456b4badfa.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1750943062951/f61cd887-9076-4060-b4d4-c58f0847facb.png
tags: docker, reactjs, dockerfile, tailwind-css, vite

---

> **Introduction**

If you’ve built a sleek, blazing-fast application with Vite + TypeScript + Tailwind CSS, the next big step is to make it deployable anywhere. In this tutorial, I’ll show you how to **Dockerize your React.js app** — making it easy to run your project in a containerised environment with just two commands.

I’ll walk you through the full process using my open-source portfolio project on GitHub.

### What We’ll Cover

* Project Overview
    
* Writing the Dockerfile
    
* Building the Docker Image
    
* Running the Container
    
* Final Testing
    

## 1\. Project Overview

Here’s what my project uses:

* **React.js** for lightning-fast development
    
* **TypeScript** for type-safe coding
    
* **Tailwind CSS** for modern UI styling
    
* **Docker** for consistent containerised deployment
    

You can find the source code here:  
👉 [GitHub Repository](https://github.com/your-username/your-repo) *(*[https://github.com/laoluafolami/portfolio-olaolu.git](https://github.com/laoluafolami/portfolio-olaolu.git)*)*

## 2\. Creating the Dockerfile

At the root of your project, create a file named `Dockerfile` (no extension):

```dockerfile
# Use an official Node.js runtime as the base image
FROM node:18-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application
COPY . .

# Build the app for production
RUN npm run build

# Install a lightweight static file server
RUN npm install -g serve

# Expose the port the app will run on
EXPOSE 4173

# Command to run the app
CMD ["serve", "-s", "dist", "-l", "4173"]
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750940722948/b2eb873d-30d2-4e60-a919-15698bc26765.png align="center")

This Dockerfile does three key things:

* Installs dependencies
    
* Builds your static app
    
* Serves it from the `dist` folder using `serve`
    

## 3\. Build the Docker Image

Open your terminal in the project directory and run:

```bash
docker build -t portfolio .
```

This will package your app into a Docker image named `portfolio`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750941303910/868b9a3f-8df8-4e95-8e77-d2965d0f7025.png align="center")

To view the image you just created, use:

```bash
docker image ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750941666594/8f491dc4-6064-4f8c-a5aa-daf26215e5e9.png align="center")

## 4\. Run the Docker Container

Now, let’s run the container and map the internal port to a local one (host machine):

```bash
docker run -d -p 4173:4173 --name portfolio- portfolio
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750941525987/0b7c7ed8-8625-413c-b087-d00979d5bcaa.png align="center")

* `-d`: Runs in detached mode
    
* `-p 4173:4173`: Maps local port 4173 to the container
    
* `--name`: Gives your container a name
    

To check the running container:

```bash
docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750941850534/195218e8-cf19-42ee-b3c0-c428b6dea4b6.png align="center")

Open your browser and visit:

```http
http://localhost:4173
```

Boom! 🎉 Your portfolio is running in Docker!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750941910446/50a56174-1cd2-4b51-b80f-792e5284cb29.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750941949863/081af055-22db-4cf3-b611-1d5f2a47d430.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750941982704/21cbff5e-2dd5-4e1d-a536-e2092072de88.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750942015240/30dee1f5-5644-4fc7-87ad-955a57672f89.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750942048819/3337813a-b935-4c70-a67a-c319eec3978f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750942072905/319ab9a6-7db3-4a25-8c28-d782e3d8ca27.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750942094610/89b2c437-dfd1-4293-9637-d5031094bc6f.png align="center")

---

## ✅ 5. Docker Cleanup (Optional)

To stop and remove your container:

```bash
docker stop portfolio
docker rm portfolio
```

To remove the image:

```bash
docker rmi portfolio
```

## Final Thoughts

Dockerising your Vite app helps you ship it anywhere with confidence, whether you're deploying to cloud platforms like AWS, Azure, or just testing locally.

---

## Let’s Connect

If you found this helpful, share it and follow me here on Hashnode for more DevOps and frontend content.