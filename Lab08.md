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



https://istio.io/latest/docs/tasks/traffic-management/request-routing/
https://istio.io/latest/docs/tasks/traffic-management/fault-injection/
https://istio.io/latest/docs/tasks/traffic-management/circuit-breaking/


Istio 流量管理 (Traffic Management) 能力的实践经验，特别是如何利用这些能力来管理微服务架构中的流量和部署。

流量转移







