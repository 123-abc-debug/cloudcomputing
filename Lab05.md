# 1.What is a container?
解决的问题：你如何确保你的应用程序所需的Python（或Node或数据库）版本不受你机器上已有内容的影响？你如何管理潜在的冲突？

https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/

容器是一种轻量级、隔离的软件打包和运行技术，它解决了“在我机器上能跑，在你机器上就报错”的环境一致性问题。
什么是容器？简单地说，容器是应用程序每个组件的独立进程。每个组件——前端React应用程序、Python API引擎和数据库——都在自己的隔离环境中运行，与机器上的其他一切完全隔离。
React 前端在一个容器中运行；
Python 后端在另一个容器中运行；
数据库在第三个容器中运行；

## Containers versus virtual machines (VMs)
容器和虚拟机的区别，我的理解是一个是创建一个虚拟的电脑，每开一个虚拟机，其实就是启动了一个完整的系统，资源开销很大（内存、CPU都要分一份）。
一个是创建进程，一个被隔离开的进程（process）。它运行时，只带上自己需要的文件、依赖和配置。所有容器共用宿主机的操作系统内核（kernel），而不是各自带一个新的系统。各自为了满足不同的目的和效率

可以把两者结合：云服务商提供的“机器”其实往往是虚拟机（VM）。

但在一台虚拟机里面，我们可以装一个容器运行环境（如 Docker）。
然后在这个虚拟机里运行多个容器化的应用。
## 如何运行一个容器？实际操作，使用GUI和CLI来操作Docker
### 介绍一下使用gui的整个过程
（1）在搜索框里面输入想要拉取的镜像，等价于docker pull <image-name>
 你可以写 docker pull welcome-to-docker（若仓库上存在同名镜像）

（2）镜像拉取成功后，给容器设置名字，点击 Run（运行）

Docker 用镜像作为模板创建容器（容器是一个可运行的实例）。容器会被分配一个唯一 ID，并准备好运行镜像内定义的默认命令（ENTRYPOINT/CMD）。
在点击 “Run” 之前，可以展开 Optional settings（可选设置） 来配置运行参数，如：

容器名称（Container name）

端口映射（Host port ↔ Container port）

环境变量（Environment variables）

数据卷挂载（Volumes）
（3）设置容器参数并运行，
docker run -d --name welcome-to-docker -p 8080:80 <image-name>
使用 CLI，可以通过一条命令完成相同的操作：
docker run -d --name welcome-to-docker -p 8080:80 welcome-to-docker
解释如下：
-d：后台运行容器（detached mode）
--name welcome-to-docker：设置容器名称
-p 8080:80：将主机 8080 端口映射到容器内 80 端口
welcome-to-docker：镜像名称
2. 点击运行，并设置容器名和主机端口（例如将容器端口80映射到主机端口8080）。
3. 运行后，可以通过浏览器访问 `http://localhost:8080`查看运行中的网页应用。

# 2.What is an image?

https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-an-image/

**容器是一个隔离的进程，但这个进程运行所需要的所有文件、配置和环境从哪里来？答案就是：镜像。**
容器本质上只是一个在宿主机上运行的进程，它被限制在自己的命名空间中，拥有独立的文件系统、网络和进程空间。
但容器本身不会凭空生成文件系统，它需要一个“模板”——这就是 容器镜像（image）

## 什么是容器镜像
容器映像是一个标准化的包，其中包括运行容器的所有文件、二进制文件、库和配置。
举个例子：
PostgreSQL 镜像
包含数据库二进制文件（postgres, initdb, psql 等）；
包含默认配置文件（postgresql.conf, pg_hba.conf）；
还包含运行所需的系统库（比如 libpq 等）。
运行后，容器内部就像一台装好了 PostgreSQL 的小服务器。

## 镜像的两个核心原则
镜像是不可变的
镜像是有多层组成，Docker 镜像并不是一个单一的大文件，而是由**多层文件系统（layers）**叠加组成的。举个例子：
| 层级      | 内容                                |
| ------- | --------------------------------- |
| Layer 1 | 基础镜像，比如 Ubuntu                    |
| Layer 2 | 安装 Python                         |
| Layer 3 | 安装 Flask 依赖                       |
| Layer 4 | 复制你的项目代码                          |
| Layer 5 | 设置启动命令 `CMD ["python", "app.py"]` |

### 实际操作的例子
你要做一个 Python 应用，不用从零开始；

直接从官方 python:3.11 镜像继承；

再添加你的依赖和代码层；

这样生成的镜像只在原有基础上“叠加”了你的改动。

## DockerHub
Docker Hub 是一个全球性的、官方的 Docker 镜像仓库（Marketplace）
举个例子：想用 Redis 或 Memcached？
直接在 Docker Hub 搜索并下载对应的官方镜像，一两秒钟就能启动服务。

## 实操
1.整个过程就是在image的dashboard里面搜索镜像和pull镜像
 “Pull” 是 Docker 中的一个核心操作，意思是：从远程镜像仓库（通常是 Docker Hub）下载镜像到本地。
“本地”指的是 Docker Engine 管理的宿主机存储区域，镜像被下载到这里，由 Docker 统一管理，而不是你电脑上的普通文件夹。

2.通过 Docker Desktop 的镜像详情页面可以查看镜像内部的一些具体信息
在 Docker Desktop 中选中某个镜像，然后进入 **Image Details（镜像详情）** 页面，你通常可以看到：

### 1. 镜像的层（Layers）
- 每一层代表镜像在某一步构建中增加、删除或修改的文件系统内容。
- 可以看到层的顺序和大小，有助于分析镜像构建和优化。

### 2. 已安装的包和库（Packages and libraries）
- 如果镜像中有包管理器（比如 `apt` 或 `pip`），Docker Desktop 会列出部分被安装的软件包。
- 有些镜像会显示版本信息，方便你确认依赖环境。

### 3. 发现的漏洞（Vulnerabilities）
- Docker Desktop 会扫描镜像已知安全漏洞（如果开启了安全扫描）。
- 可以帮助开发者判断镜像是否安全，是否需要更新。


## 自己探索里面的东西
通过 Docker Desktop 的 Containers → Files 页面，你可以像在资源管理器中一样浏览容器的内部文件系统，看到容器隔离环境里的内容，而不会影响你的本地系统。



**镜像是一个标准化的软件包**，它包含了运行一个容器所需的一切：

- **文件**（你的应用代码）
- **二进制程序**（如 Python、Node.js 的解释器）
- **库文件**（应用依赖的第三方库）
- **配置文件**



https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-docker-compose/


# What is Docker Compose?
解决的问题：运行多个容器？如果你运行多个，你如何将它们连接在一起？

举个例子：
但现实应用通常更复杂，会用到多个服务，例如：
数据库（PostgreSQL、MySQL）
消息队列（RabbitMQ、Kafka）
缓存（Redis、Memcached）
Web 后端（Python、Node.js）
前端（React、Vue 等）

### docker compose是一个工具，用来管理多容器应用
举个例子来说明优势
集中管理
web 和 db 两个容器都在同一个 YAML 文件中定义。
团队成员只需 clone 仓库，就能用同一个文件启动完整应用。

声明式（Declarative）

YAML 文件中定义了希望的状态：web 容器连接 db，端口映射、环境变量、数据卷等。

修改配置后再次执行：

docker compose up -d


Compose 会智能应用更改，不必手动删除重建。

简化多容器操作

不用手动启动 docker run 多次，也不用手动配置网络。

停止和清理整个应用只需一条命令：

docker compose down

### difference between dockerfile 和 compose
| 文件类型                   | 用途                                                 |
| ---------------------- | -------------------------------------------------- |
| **Dockerfile**         | 描述 **如何构建一个容器镜像**（例如安装 Python、依赖包、复制代码）。           |
| **docker-compose.yml** | 描述 **运行哪些容器以及如何运行**（包括网络、端口、依赖关系）。                 |
| **联系**                 | Compose 文件可以引用 Dockerfile 来构建某个服务的镜像，然后再用这个镜像启动容器。 |

Dockerfile：构建你的 Python 应用镜像
docker-compose.yml：启动 Python Web 服务 + PostgreSQL 数据库 + Redis 缓存，并把它们连接在同一个网络里
### 集中管理
- `web` 和 `db` 两个容器都在同一个 YAML 文件中定义。
- 团队成员只需 clone 仓库，就能用同一个文件启动完整应用。

### 声明式（Declarative）
- YAML 文件中定义了希望的状态：`web` 容器连接 `db`，端口映射、环境变量、数据卷等。
- 修改配置后再次执行：
```bash
docker compose up -d


## 实验，使用docker来运行一个多容器的应用


https://docs.docker.com/get-started/docker-concepts/running-containers/publishing-ports/


https://docs.docker.com/get-started/docker-concepts/running-containers/overriding-container-defaults/
https://docs.docker.com/get-started/docker-concepts/running-containers/persisting-container-data/
https://docs.docker.com/get-started/docker-concepts/running-containers/sharing-local-files/
https://docs.docker.com/get-started/docker-concepts/running-containers/multi-container-applications/


Please write a document with screenshots and notes and commit it to your github repo.

Recommendations:
https://docs.docker.com/desktop/install/windows-install/
https://docs.docker.com/desktop/wsl/





1.https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/



`docker run` → 创建并启动容器

`-d` → 后台运行

`-p 宿主机端口:容器端口` → 端口映射

`docker/welcome-to-docker` → 镜像名称



![image-20250924085523178](D:\.殷宇昂文件夹\.数学建模\微分方程总结\2024B代码\2020A题\革制品\云计算\Lab\Lab05.assets\image-20250924085523178.png)

![image-20250924090052101](D:\.殷宇昂文件夹\.数学建模\微分方程总结\2024B代码\2020A题\革制品\云计算\Lab\Lab05.assets\image-20250924090052101.png)



stop the docker

![image-20250924090252950](D:\.殷宇昂文件夹\.数学建模\微分方程总结\2024B代码\2020A题\革制品\云计算\Lab\Lab05.assets\image-20250924090252950.png)

容器镜像 (Image)

**镜像 (Image)** 就是打包好这些内容的标准包。

镜像来源：Docker Hub

![image-20250924091023519](D:\.殷宇昂文件夹\.数学建模\微分方程总结\2024B代码\2020A题\革制品\云计算\Lab\Lab05.assets\image-20250924091023519.png)



https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-docker-compose/

它清晰地解释了 Compose 要解决的核心问题、其工作原理和基本用法。

**Docker Compose 是一个用于定义和运行多容器 Docker 应用程序的工具**。当你的应用需要多个服务（如前端、后端、数据库、缓存等）时，它让你无需手动管理每个容器，而是通过一个声明式的 YAML 文件来统一配置和启动所有服务。

Compose 通过一个 **`compose.yaml`文件** 解决上述所有问题。可以在单个YAML文件中定义所有容器及其配置，Compose是一个声明性工具——你只需定义它并执行即可

dockerfile的样子

使用Python官方镜像作为基础

FROM python:3.9-slim

设置工作目录

WORKDIR /app

将当前目录的文件复制到容器的 /app 目录下

COPY . .

安装依赖：Flask 和 Redis 客户端库

RUN pip install flask redis

设置容器启动时自动运行的命令

CMD ["python", "app.py"]

### compose的样子

version: '3.8'

services:

定义 Web 应用服务

  web:
    build: .  # 关键！这告诉Compose：web服务的镜像，需要根据当前目录的 Dockerfile 来构建。
    ports:
      - "5000:5000"  # 端口映射
    depends_on:
      - redis  # 明确告知Compose：web服务依赖于redis服务，请先启动redis。

定义 Redis 服务

  redis:
    image: "redis:alpine"  # 直接使用Docker官方提供的Redis镜像，无需自己写Dockerfile。



### 尝试

您将使用一个使用Node.js和MySQL构建的简单待办事项列表应用程序作为数据库服务器。

1.下载安装docker桌面

2.克隆to-do-list的链接

![image-20251015081439812](D:\.殷宇昂文件夹\.数学建模\微分方程总结\2024B代码\2020A题\革制品\云计算\Lab\Lab05.assets\image-20251015081439812.png)

compose.yaml代码解释

![image-20251015082457836](D:\.殷宇昂文件夹\.数学建模\微分方程总结\2024B代码\2020A题\革制品\云计算\Lab\Lab05.assets\image-20251015082457836.png)

**`services` (服务)：** 定义了您想要运行的独立容器。这里定义了 `app` (Node.js) 和 `mysql` 两个服务。

**`volumes` (卷)：** 定义了用于持久化数据的存储区域。这里定义了 `todo-mysql-data` 卷来保存数据库数据。





https://docs.docker.com/get-started/docker-concepts/running-containers/publishing-ports/


https://docs.docker.com/get-started/docker-concepts/running-containers/overriding-container-defaults/


https://docs.docker.com/get-started/docker-concepts/running-containers/persisting-container-data/



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



https://docs.docker.com/get-started/docker-concepts/running-containers/sharing-local-files/



https://docs.docker.com/get-started/docker-concepts/running-containers/multi-container-applications/


Please write a document with screenshots and notes and commit it to your github repo.

Recommendations:
https://docs.docker.com/desktop/install/windows-install/
https://docs.docker.com/desktop/wsl/



3.**Docker Compose** 是一个声明式工具（declarative tool）：

​	用 **YAML 文件** 定义多个容器及其配置（镜像、端口、卷、网络等）。





