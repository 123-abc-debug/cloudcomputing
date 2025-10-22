This lab exercise will give you hands-on experience with Istio's traffic management capabilities. For example, you can demonstrate how the traffic shifting can be used to manage deployments and migrations of service versions in a microservices architecture.

For the following four topics, please submit a word or pdf document containing your compiled screenshots for the key steps.  
1.流量转移
https://istio.io/latest/docs/tasks/traffic-management/traffic-shifting/
此任务向您展示如何将流量从微服务的一个版本转移到另一个版本。

一个常见的用例是将流量从旧版本的微服务逐步迁移到新版本。在 Istio 中，您可以通过配置一系列路由规则来实现此目标，这些规则将一定比例的流量从一个目标重定向到另一个目标。

在此任务中，您将使用 50% 的流量发送至 reviews:v1 ，50% 的流量发送至 reviews:v3 。然后，您将通过将 100% 的流量发送至 reviews:v3 来完成迁移。

（1）在开始之前应该做什么
Setup Istio by following the instructions in the Installation guide.
按照以下说明设置 Istio 安装指南 。

Deploy the Bookinfo sample application.
部署 Bookinfo 示例应用程序。

前面两步都完成了

Review the Traffic Management concepts doc.
查看交通管理概念文档。
流量管理的概念：stio 流量管理的核心目标是提供对服务间请求流动的 精细控制

首先介绍一下
# 第一个，应用基于权重的路由
（1）首先，运行此命令将所有流量路由到 v1 版本

kubectl apply -f samples/bookinfo/networking/destination-rule-all.yaml

<img width="1279" height="609" alt="image" src="https://github.com/user-attachments/assets/75097116-c913-4d62-8c34-159cf1229592" />


kubectl apply -f samples/bookinfo/networking/virtual-service-all-v1.yaml

请注意，无论刷新多少次，页面的评论部分都不会显示任何星级评分。这是因为您将 Istio 配置为将评论服务的所有流量路由到版本 reviews:v1 ，而此版本的服务不访问星级评分服务。
<img width="1032" height="978" alt="image" src="https://github.com/user-attachments/assets/fbad5b7a-0910-4e1f-a25e-695a78002108" />

kubectl apply -f samples/bookinfo/networking/virtual-service-reviews-50-v3.yaml

使用以下命令将 50% 的流量从 reviews:v1 转移到 reviews:v3 

刷新浏览器中的 /productpage 页面，现在大约有 50% 的几率会看到红色的星级评分。这是因为 v3 版的 reviews 访问了星级评分服务，而 v1 版没有。
<img width="1271" height="599" alt="image" src="https://github.com/user-attachments/assets/43e498b4-a5c3-4ca9-8914-9b26e50b0ea5" />


<img width="1069" height="935" alt="image" src="https://github.com/user-attachments/assets/ef0d1b9b-87f0-4402-af1d-c45ae21ada78" />


假设您确定 reviews:v3 微服务是稳定的，您可以通过应用此虚拟服务将 100% 的流量路由到 reviews:v3 ：
kubectl apply -f samples/bookinfo/networking/virtual-service-reviews-v3.yaml

<img width="1116" height="58" alt="image" src="https://github.com/user-attachments/assets/0e6f06e9-7a62-4554-9b35-8fa09ae18121" />

（2）接着是删除
删除应用程序路由规则
kubectl delete -f samples/bookinfo/networking/virtual-service-all-v1.yaml
<img width="1109" height="121" alt="image" src="https://github.com/user-attachments/assets/92b262ce-280b-4c21-b3c6-2246d7fb41e5" />

# 请求路由

https://istio.io/latest/docs/tasks/traffic-management/request-routing/




https://istio.io/latest/docs/tasks/traffic-management/fault-injection/
https://istio.io/latest/docs/tasks/traffic-management/circuit-breaking/


Istio 流量管理 (Traffic Management) 能力的实践经验，特别是如何利用这些能力来管理微服务架构中的流量和部署。

流量转移







