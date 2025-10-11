### (a)	Describe the three primary cloud service models in cloud computing鈥擨nfrastructure as a Service (IaaS), Platform as a Service (PaaS), and Software as a Service (SaaS). Provide specific examples of how each model can be applied in the context of software development.
#### Infrastructure as a Service (IaaS)

​	IaaS provides the most fundamental computing resources. It is like renting a "bare" virtual computer (a virtual machine), storage, and networking equipment online. You are responsible for managing the operating system, runtime environments, middleware, and applications.
​	Application Example in Software Development:
​	Scenario: A development team needs to build a complex, highly customized website that requires specific versions of an operating system and database, and demands complete control over the underlying system.
​	How it's applied: They can rent an EC2 (Elastic Compute Cloud) virtual machine instance from AWS (Amazon Web Services). On this virtual machine, they must install the Linux/Windows operating system, configure a web server (like Nginx/Apache), install a database (like MySQL), deploy their application code, and set up firewall rules. IaaS offers the greatest flexibility and control but also carries the heaviest operational burden.

#### Platform as a Service (PaaS)

​	PaaS provides a complete software development and deployment environment. It is like renting a fully-furnished and utilities-connected "studio" online. You no longer need to care about virtual machines, operating systems, or runtime environments; you only need to focus on writing and deploying your application code itself.
​	Application Example in Software Development:
​	Scenario: A team wants to quickly develop and launch a web application using the Python Django framework and does not want to waste time configuring servers and databases.
​	How it's applied: They can use Heroku or Google App Engine (GAE). They simply push their written Django code to the platform (e.g., via git push heroku main), and the PaaS platform automatically handles all the underlying work: preparing the operating system, installing the Python environment, configuring the web server, and providing a companion database service. Developers are completely freed from infrastructure management.

#### Software as a Service (SaaS)

​	SaaS provides fully developed, ready-to-use applications. It is like directly "using" software online, typically accessed through a web browser. You manage nothing; you only need to register an account and start using it.
​	Application Example in Software Development:
​	Scenario: A development team needs a project management tool to track progress, a code repository to host code, and a communication tool for daily interaction.
​	How it's applied: They directly register for and use Trello or Jira (project management SaaS), GitHub or GitLab (code repository SaaS), and Slack or Teams (collaboration SaaS). They don't need to install any software and are completely unaware of and unconcerned with which servers the software runs on; they only need to focus on the software's functionality.


### (b)What is Docker? Describe a scenario where you would use containerization technologies such as Docker in software development. How does containerization contribute to the development and deployment process of software in this scenario?


#### What is Docker?

​	You can think of Docker as a software "packaging box". It packs your application, code, settings, and all necessary dependent libraries into a standard, portable "container". This container can run in exactly the same way on any computer.

#### When would you use it? (Scenario)

​	Imagine your team is collaborating to develop a website. Your friend codes the login page in Python, you build the search feature in Node.js, and another teammate uses Java for the payment system. Getting all these different parts, built with different technologies, to work together on everyone's computer (and later on the server) can be a major headache because everyone's software versions and runtime environments might be different.

#### How does it help?

​	Docker solves this problem. Each member can package the part they developed into an independent container. These containers are like self-contained "bubbles". Everyone can then easily share and run these "bubbles". This means:
​	The program runs exactly the same on your laptop, your friend's Mac, and the server.
​	You just need to share the container with others, and it can run instantly on any computer that has Docker installed.

### (c) Deploy n8n (n8n.io) with Docker and capture a screenshot of http://127.0.0.1:5678. Please explain the docker command in detail.
docker run -d --name n8n -p 5678:5678 -p 5679:5679 n8nio/n8n
| **Parameter**      | **Purpose & Explanation**                                    |
| :----------------- | :----------------------------------------------------------- |
| **`docker run`**   | The core Docker command used to create and start a new container from an image. |
| **`-d`**           | Runs the container in **detached mode** (in the background). This returns control to your terminal after starting the container. |
| **`--name n8n`**   | Assigns the name **`n8n`** to the container. This name is used for easy management (e.g., to start, stop, or view logs). |
| **`-p 5678:5678`** | **Port mapping.** Binds port `5678`on your **local machine (host)** to port `5678`**inside the container**. This allows you to access the n8n web interface at `http://127.0.0.1:5678`. |
| **`-p 5679:5679`** | **Port mapping.** Binds port `5679`on your host to port `5679`inside the container. This port is used for n8n's **advanced features, such as its waiting workflow functionality**. |
| **`n8nio/n8n`**    | Specifies the **Docker image** to use. Docker will download the official `n8nio/n8n`image from Docker Hub if it is not already present on your system. |
<img width="796" height="336" alt="image" src="https://github.com/user-attachments/assets/3162038a-8fd7-4678-8e8f-5762696919c2" />

<img width="812" height="383" alt="image" src="https://github.com/user-attachments/assets/76807a0a-36ee-4afb-927c-6190df1ae831" />

docker ps  ：

 This command lists all currently **running** Docker containers. You can use it to verify that your `n8n`container is active and its status is `Up`.

docker logs n8n ：This command fetches and displays the log output from the `n8n`container. Logs are crucial for troubleshooting startup errors, checking the initialization process, and seeing the general activity of the application inside the container.
<img width="1661" height="660" alt="image" src="https://github.com/user-attachments/assets/c8e77a4b-71f1-48eb-8c8c-d614c104c76a" />



