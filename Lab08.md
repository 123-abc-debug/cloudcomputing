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

此任务的初始目标是应用规则，将所有流量路由到微服务的 v1 （版本 1）。稍后，您将应用规则，根据 HTTP 请求标头的值来路由流量。这里的意思是自己来控制路由的流量吗

（1）首先，路由至版本一
Istio 使用虚拟服务来定义路由规则。运行以下命令应用虚拟服务，将所有流量路由到每个微服务的 v1 ：
kubectl apply -f samples/bookinfo/networking/virtual-service-all-v1.yaml
强制将所有流量路由到 v1版本

kubectl get virtualservices -o yaml
kubectl get destinationrules -o yaml

应用一个 VirtualService（虚拟服务）配置​​ 到 Kubernetes 集群
​​列出当前集群中的所有 VirtualService 资源​​
列出当前集群中的所有 DestinationRule 资源
 
（2）接着，测试新的路由配置
您可以通过再次刷新 /productpage 轻松测试新配置 浏览器中的 Bookinfo 应用程序。 请注意，页面的评论部分没有显示评级星，没有 无论刷新多少次。这是因为您已将 Istio 配置为路由 所有评论服务的流量都流向版本 reviews:v1 ，并且此版本的服务不访问星级评分服务。
<img width="1083" height="682" alt="image" src="https://github.com/user-attachments/assets/b3d39a95-e696-4a0e-9c58-4e5d6e44423d" />

（3）基于用户身份的路由

接下来，您将更改路由配置，以便将来自特定用户的所有流量路由到特定服务版本。在本例中，来自名为 Jason 的用户的所有流量都将被路由到服务 reviews:v2 。
请记住， reviews:v2 是包含星级评定功能的版本。

现在使用jason登录
<img width="2079" height="518" alt="image" src="https://github.com/user-attachments/assets/592af542-14ff-4875-afd0-02b9534be019" />

最后，了解发生了什么
在此任务中，您使用 Istio 将 100% 的流量发送到每个 Bookinfo 服务的 v1 版本。然后，您设置了一条规则，根据 productpage 服务添加到请求中的自定义 end-user 标头，选择性地将流量发送到 reviews 服务的 v2 版本。
Note that Kubernetes services, like the Bookinfo ones used in this task, must adhere to certain restrictions to take advantage of Istio’s L7 routing features. Refer to the Requirements for Pods and Services for details.
请注意，Kubernetes 服务（例如本任务中使用的 Bookinfo 服务）必须遵守某些限制才能利用 Istio 的 L7 路由功能。有关详细信息，请参阅 Pod 和服务的要求 。

In the traffic shifting task, you will follow the same basic pattern you learned here to configure route rules to gradually send traffic from one version of a service to another.
在流量转移任务中，您将遵循在此处学习的相同基本模式来配置路由规则，以逐步将流量从服务的一个版本发送到另一个版本。

# 故障注入
https://istio.io/latest/docs/tasks/traffic-management/fault-injection/

此任务向您展示如何注入故障来测试应用程序的弹性。
（1）首先，注入一个可以解决的故障
为了测试 Bookinfo 应用微服务的弹性，我们在 reviews:v2 和 ratings 微服务之间为用户 jason 注入了 7 秒的延迟。此测试将发现 Bookinfo 应用中故意引入的一个 bug。reviews:v2 服务对 ratings 服务的调用设置了 10 秒的硬编码连接超时。即使您引入了 7 秒的延迟，您仍然希望端到端流程能够顺利进行，不会出现任何错误。
 当我用jason登录的时候,会出现问题
<img width="1191" height="465" alt="image" src="https://github.com/user-attachments/assets/783809a7-c7e9-4340-b2de-159775bf9985" />

查看网页响应时间
<img width="2473" height="369" alt="image" src="https://github.com/user-attachments/assets/4f9ee356-f9f0-4e15-a0d9-d8dd052464e4" />
（2）了解背后发生了什么，
正如预期的那样，您引入的 7 秒延迟不会影响 reviews 服务，因为 reviews 和 ratings 服务之间的超时时间硬编码为 10 秒。然而， productpage 和 reviews 服务之间也存在硬编码的超时时间，代码为 3 秒 + 1 次重试，总共 6 秒。因此， productpage 对 reviews 服务的调用会提前超时，并在 6 秒后抛出错误。
（3）如何修复bug
Either increasing the productpage to reviews service timeout or decreasing the reviews to ratings timeout
增加 productpage 到 reviews 服务的超时时间，或减少 reviews 到 ratings 超时时间
Stopping and restarting the fixed microservice
停止并重新启动已修复的微服务
Confirming that the /productpage web page returns its response without any errors.
确认 /productpage 网页返回其响应且没有任何错误。


第二部分注入 HTTP 中止故障
测试微服务弹性的另一种方法是引入 HTTP 中止故障。在本任务中，您将为测试用户 jason 的 ratings 微服务引入 HTTP 中止。

In this case, you expect the page to load immediately and display the Ratings service is currently unavailable message.
在这种情况下，您希望页面立即加载并显示 Ratings service is currently unavailable 消息。

kubectl apply -f samples/bookinfo/networking/virtual-service-ratings-test-abort.yaml
<img width="1043" height="665" alt="image" src="https://github.com/user-attachments/assets/2f4ffcce-70ec-4272-a526-62c447c3c984" />


# Circuit Breaking  熔断

https://istio.io/latest/docs/tasks/traffic-management/circuit-breaking/
此任务向您展示如何配置连接、请求和异常值检测的断路。

熔断是创建弹性微服务应用程序的重要模式。熔断允许您编写应用程序以限制故障、延迟峰值以及网络特性的其他不良影响。

In this task, you will configure circuit breaking rules and then test the configuration by intentionally “tripping” the circuit breaker.
在此任务中，您将配置断路规则，然后通过有意“跳闸”断路器来测试配置。

（1）首先，启动httpbin实例

（2）接着，Configuring the circuit breaker配置断路器
<img width="1430" height="509" alt="image" src="https://github.com/user-attachments/assets/abd32c14-de01-4341-81dc-3c7faa429b2e" />


（3）然后，添加客户端
创建一个客户端来向 httpbin 服务发送流量。该客户端是一个简单的负载测试客户端，名为 fortio 。Fortio 允许您控制传出 HTTP 调用的连接数、并发数和延迟。您将使用此客户端来“触发”您在 DestinationRule 中设置的熔断策略。

<img width="1559" height="812" alt="image" src="https://github.com/user-attachments/assets/1057d4d2-2d44-48d6-80b8-75cb17a73c9a" />

（4）接着，Tripping the circuit breaker
断路器跳闸
在 DestinationRule 设置中，您指定了 maxConnections: 1 和 http1MaxPendingRequests: 1 . 这些规则表明，如果您超过 一个连接和一个请求同时发生，你应该看到一些失败的情况 istio-proxy 为进一步的请求和连接打开了电路。
kubectl exec "$FORTIO_POD" -c fortio -- /usr/bin/fortio load -c 2 -qps 0 -n 20 -loglevel Warning http://httpbin:8000/get


<img width="952" height="665" alt="image" src="https://github.com/user-attachments/assets/15e8a8fd-443a-403b-8d81-b9f8201aca36" />

<img width="1198" height="850" alt="image" src="https://github.com/user-attachments/assets/adce122e-451c-498e-8956-c32815471cae" />
这里能看到什么时候熔断
<img width="915" height="93" alt="image" src="https://github.com/user-attachments/assets/4c4ee963-c477-483c-8495-bc681dc2588f" />



