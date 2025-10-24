# Lab05:Docker Core Concepts Tutorial & Notes
# 1️.What is a Container?
## The Problem It Solves

> How do you ensure that the version of Python (or Node, or Database) your application needs is not affected by what’s already installed on your machine?  
> How do you manage potential conflicts between different environments?

🔗 Reference: [What is a container? (Docker Documentation)](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/)

---

## Definition

A **container** is a lightweight, isolated software packaging and execution technology.  
It solves the famous problem:

> “It works on my machine, but not on yours.”

Simply put:
- A container is an **independent process environment** for an application.
- Each component (e.g., frontend, backend, database) runs in its own container.
- Containers are **isolated** from one another and from the host system.

Example:
- The **React frontend** runs inside one container.  
- The **Python backend** runs in another container.  
- The **Database** runs in a third container.  

Each container includes all dependencies, configuration, and files it needs — ensuring consistent behavior across machines.

---

## Containers vs Virtual Machines (VMs)

| Comparison Aspect | Containers | Virtual Machines (VMs) |
|-------------------|-------------|--------------------------|
| Startup Speed | Seconds | Minutes |
| Resource Usage | Lightweight, shares host OS kernel | Heavy, each VM includes its own OS |
| Isolation Level | Process-level | System-level |
| Typical Use Case | Microservices, CI/CD | Cloud servers, multi-OS environments |

### Conceptual Difference

- **Virtual Machines (VMs):**  
  Create a *virtual computer* with its own full operating system.  
  Each VM consumes CPU, memory, and disk resources — heavier and slower.

- **Containers:**  
  Create *isolated processes* that share the same host OS kernel.  
  They include only what’s necessary to run the app — faster and lighter.

### Cobined Use Case

They can complement each other:
- Cloud providers often offer **virtual machines**.
- Inside one VM, you can install **Docker** to run multiple **containers**.

---

## Try it Out: How to Run a Container (Using GUI and CLI)
In this hands-on, you will see how to run a Docker container using the Docker Desktop GUI.
### Using the GUI (Docker Desktop)

<img width="1592" height="629" alt="image" src="https://github.com/user-attachments/assets/2e0ea33e-f05d-4ee7-8818-6719567884d5" />

<img width="1647" height="1390" alt="image" src="https://github.com/user-attachments/assets/9bd6e0b7-1d52-4f94-9502-b18df99a2d5d" />

<img width="1662" height="1197" alt="image" src="https://github.com/user-attachments/assets/1425e2e7-63b9-4819-a602-b3435b3755a4" />

<img width="1233" height="168" alt="image" src="https://github.com/user-attachments/assets/35c12929-ce0b-4ff9-8631-ee5bb1113452" />



# 2. What is an Image?

Reference: [What is an image? (Docker Documentation)](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-an-image/)

---

##  What Is a Container Image?

A **container image** is a **standardized package** that includes everything needed to run a container:
- Application files and binaries  
- System libraries and dependencies  
- Configuration files  

Think of it as a **blueprint** for creating containers.

---

### Example: The PostgreSQL Image

A PostgreSQL image includes:
- Database binaries (`postgres`, `initdb`, `psql`, etc.)  
- Default configuration files (`postgresql.conf`, `pg_hba.conf`)  
- Required system libraries (e.g., `libpq`)  

When you start a container from this image,  
the container behaves just like a mini server with PostgreSQL preinstalled and ready to use.

---

## Two Core Principles of Images

### Images Are Immutable
Once built, an image **cannot be changed**.  
If you need to modify it, you build a **new image layer** on top of the existing one.

### Images Are Layered

Docker images are **composed of multiple filesystem layers**, not a single large file.  
Each layer represents a specific modification or addition.

| Layer | Description |
|--------|--------------|
| Layer 1 | Base image (e.g., Ubuntu) |
| Layer 2 | Install Python |
| Layer 3 | Install Flask dependencies |
| Layer 4 | Copy your project source code |
| Layer 5 | Set the startup command `CMD ["python", "app.py"]` |

These layers stack together to form the complete image.  
This design saves space and improves efficiency — layers can be shared across different images.

---

## Try it out:search and pull a container image using the Docker Desktop GUI.

<img width="1547" height="558" alt="image" src="https://github.com/user-attachments/assets/043b43b4-502d-43dc-b5e6-f6a6de5befcd" />
<img width="1194" height="1117" alt="image" src="https://github.com/user-attachments/assets/45876aea-aa39-4cb2-8627-a381d6e0b416" />


# 3.What is Docker Compose?

📖 Source: [Docker Docs — What is Docker Compose?](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-docker-compose/)

## Background
In previous examples, we’ve only worked with **single-container applications**.  
However, real-world projects often need **multiple components**, such as:
- Databases (MySQL, PostgreSQL)
- Message queues (RabbitMQ, Kafka)
- Caches (Redis, Memcached)
- Web backends (Node.js, Python Flask/Django)
- Frontend services (React, Vue)

So the question arises:  
> Should we install everything in a single container, or run multiple containers?  
> If multiple, how do we connect them all together?

---

## Best Practice for Container Design
> “**Each container should do one thing, and do it well.**”

Each container should handle one specific function, for example:
- One container runs the web service  
- One container runs the database  
- One container runs the cache  

### Benefits:
- **Modular design** — easy to maintain  
- **Independent scaling or updating** — modify one service without affecting others  
- **Improved stability and security**

---


## Docker Compose Makes It Simple

With **Docker Compose**, everything becomes much easier.

You can define **all your containers** (called *services*) and their configurations in a single **YAML file**.

Then, start everything with just **one command**:
docker compose up -d


### Dockerfile vs docker-compose.yml

| File Type              | Purpose                                                                                          |
| ---------------------- | ------------------------------------------------------------------------------------------------ |
| **Dockerfile**         | Defines **how to build an image** (install dependencies, copy code, set startup commands).       |
| **docker-compose.yml** | Defines **how to run multiple containers** (including networks, ports, and dependencies).        |
| **Relationship**       | The Compose file often references a Dockerfile to build the image needed for a specific service. |


## Try it out 
Use a Docker Compose to run a multi-container application. You'll use a simple to-do list app built with Node.js and MySQL as a database server.

Open a terminal and clone this sample application.git clone https://github.com/dockersamples/todo-list-app


<img width="1668" height="1267" alt="image" src="https://github.com/user-attachments/assets/6ec3d584-40bb-480f-a90f-2695cd33017e" />


<img width="1045" height="1155" alt="image" src="https://github.com/user-attachments/assets/529b73df-6cb3-447b-93fc-444b59ac636d" />


Use the docker compose up command to start the application:
<img width="1281" height="182" alt="image" src="https://github.com/user-attachments/assets/d8c4d9c5-41f7-452a-9a1f-5390d1f5990a" />

open http://localhost:3000 in the browser to see the site
<img width="728" height="613" alt="image" src="https://github.com/user-attachments/assets/bd30af23-79b8-472d-8152-d655fa8190fd" />

look at the Docker Desktop GUI

<img width="1861" height="215" alt="image" src="https://github.com/user-attachments/assets/22089572-65ed-40ac-a7ca-012277474065" />

use the docker compose down command to remove everything
<img width="1925" height="149" alt="image" src="https://github.com/user-attachments/assets/a71580fb-06b4-4393-9666-35bb6a974b2d" />

If you do want to remove the volumes, add the --volumes flag when running the docker compose down command
<img width="1926" height="126" alt="image" src="https://github.com/user-attachments/assets/49737818-66b8-4756-a762-b053d726e89a" />




# Persisting container data

https://docs.docker.com/get-started/docker-concepts/running-containers/persisting-container-data/
卷是一种存储机制，它能够在单个容器的生命周期之外持久化数据。可以将其想象成提供从容器内部到容器外部的快捷方式或符号链接。

这里就是创建一个卷，会有结果





# Sharing local files with containers
这个的目的是把docker1里面的内容传递到本地，但是把本地文件分享给docker有风险
将此类敏感信息直接存储在容器映像中会带来安全风险，特别是在映像共享期间。为了应对这一挑战，Docker提供了存储选项，弥合了容器隔离和主机数据之间的差距。
Docker提供了两种主要的存储选项，用于在主机和容器之间持久化数据和共享文件：卷和绑定挂载。

容器volume和bind mounts的区别

用 bind mount 或挂载主机目录给容器时，需要注意主机文件／目录的权限，否则容器可能无权访问这些文件。

## 实操
输入
docker run -d -p 8080:80 --name my_site httpd:2.4
<img width="1414" height="224" alt="image" src="https://github.com/user-attachments/assets/de8588c2-ebf1-4247-8f33-b8f779bdd753" />

delete my_site container
<img width="1207" height="385" alt="image" src="https://github.com/user-attachments/assets/17cd6a77-f15e-4eb4-8b57-77c6a273f8a1" />

选择使用另一种方式来启动
docker run -d --name my_site -p 8080:80 -v .:/usr/local/apache2/htdocs/ httpd:2.4

<img width="893" height="546" alt="image" src="https://github.com/user-attachments/assets/484a96e9-42c9-4a12-a459-d086890128ab" />

这里是展示一个双向bind的机制
Bind Mount 的特性​​
​​实时双向同步​​：主机和容器内的文件会完全同步，任何一方的修改都会立即反映在另一方。
​​删除文件的影响​​：
如果你在主机删除 index.html，容器内的 /usr/local/apache2/htdocs/index.html也会​​立刻消失​​。
Docker Desktop 的 GUI 文件浏览器（“Files”标签）会显示容器内文件的实时状态，所以删除后这里也会看不到文件。

<img width="1358" height="273" alt="image" src="https://github.com/user-attachments/assets/262d4539-ac3a-4bd1-99d3-bbf866f3f1d4" />
<img width="1066" height="184" alt="image" src="https://github.com/user-attachments/assets/fde92e86-89e5-40dc-9228-034e9eab4e5b" />





# Multi-container applications
## 解决的问题，就是关于很多应用程序都要一个个部署，很麻烦，这时 Docker Compose 就可以发挥作用了。

通过利用 Docker Compose 运行多容器设置，您可以构建以模块化、可扩展性和一致性为核心的复杂应用程序。

## 实操
Navigate into the nginx directory to build the image by running the following command:
通过运行以下命令导航到 nginx 目录来构建映像：
（1）首先，克隆仓库和构建镜像

 docker build -t nginx .
Navigate into the web directory and run the following command to build the first web image:
导航到 web 目录并运行以下命令来构建第一个 web 图像：


 docker build -t web .
先构建两个镜像
（2）接着运行容器
在运行多容器应用程序之前，你需要创建一个网络，以便所有容器之间进行通信。你可以使用 docker network create 网络
docker network create sample-app

具体的操作：
1.创建一个网络
docker network create sample-app
2.启动redis容器
docker run -d  --name redis --network sample-app --network-alias redis redis
3.下面来启动容器
docker run -d --name web1 -h web1 --network sample-app --network-alias web1 web

docker run -d --name web2 -h web2 --network sample-app --network-alias web2 web
docker run -d --name nginx --network sample-app  -p 80:80 nginx


上面的配置比较复杂，可以Simplify the deployment using Docker Compose
如前所述，使用 Docker Compose，您无需运行多个 docker run 命令。您只需在一个名为 compose.yml 的 YAML 文件中定义整个多容器应用程序即可。

就是配置compose.yaml的文件来设置






https://docs.docker.com/get-started/docker-concepts/running-containers/sharing-local-files/



https://docs.docker.com/get-started/docker-concepts/running-containers/multi-container-applications/


Please write a document with screenshots and notes and commit it to your github repo.

Recommendations:
https://docs.docker.com/desktop/install/windows-install/
https://docs.docker.com/desktop/wsl/



3.**Docker Compose** 是一个声明式工具（declarative tool）：

​	用 **YAML 文件** 定义多个容器及其配置（镜像、端口、卷、网络等）。





