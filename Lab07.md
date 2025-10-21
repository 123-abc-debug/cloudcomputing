Please follow the instructions and the complete the tasks listed  here:

https://istio.io/latest/docs/setup/getting-started/

Please collect screenshots into a word document and commit it to your github link.
如何使用istio
(1)首先，需要准备好一个 Kubernetes 集群才能继续。如果您没有集群，可以使用 kind 或任何其他受支持的 Kubernetes 平台 。
(2)接着，就是下载istio的过程，
具体步骤就是先下载包，我的windows操作系统，下载好了
<img width="1008" height="138" alt="image" src="https://github.com/user-attachments/assets/63da409d-40ea-48ba-8b21-ff9ffc7ecbbf" />
接下来就是进入到里面的sample bin的目录，把这个目录能够让被电脑自己识别到
<img width="851" height="374" alt="image" src="https://github.com/user-attachments/assets/ab0fe16a-87fa-481c-9609-ea50046bf79f" />
将 istioctl 客户端添加到您的路径，已经配置好了
<img width="1480" height="163" alt="image" src="https://github.com/user-attachments/assets/0e906cc5-1cf5-4a6b-9a0b-21d2d37b9ada" />
总结：这一阶段是为了：

获取 Istio 的客户端工具 (istioctl)、示例文件 (samples/) 和配置文件。

使 istioctl 命令在您的命令行中可用。

上面那是下载istio的一个软件包,下面要进行的是安装
（1）首先，将 Istio 的核心组件（Istiod 控制面、配置等）安装到您的 Kubernetes 集群中：
$ istioctl install -f samples/bookinfo/demo-profile-no-gateways.yaml -y
它使用了您在第一阶段配置好的 istioctl 工具。

它根据指定的配置文件（demo-profile-no-gateways.yaml）在您的 Kubernetes 集群中创建 Istio 的各种资源（如部署 Istiod Pod、配置 Webhook 等）。
<img width="1951" height="663" alt="image" src="https://github.com/user-attachments/assets/943d618b-7ce3-40c8-ac37-bd6695ff461a" />



（2）接着，添加命名空间标签，以指示 Istio 稍后部署应用程序时自动注入 Envoy sidecar 代理
kubectl label namespace default istio-injection=enabled

<img width="1900" height="94" alt="image" src="https://github.com/user-attachments/assets/93d6c36f-c7d8-4b57-8e8b-a87a3ae02912" />

目的：请在这个区域（default 命名空间）内，为你接下来的所有应用自动穿上你的‘盔甲’（Envoy 代理），以便进行统一管理和控制。
让新应用一出生就自带强大的网络和安全能力。

（3）然后，安装 Kubernetes Gateway API CRD

The Kubernetes Gateway API CRDs do not come installed by default on most Kubernetes clusters, so make sure they are installed before using the Gateway API.
大多数 Kubernetes 集群上默认不会安装 Kubernetes Gateway API CRD，因此请确保在使用 Gateway API 之前已安装它们。

Kubernetes Gateway API 是干什么的？
它的核心功能是管理和控制 流入 (Inbound/Ingress) 和 流出 (Outbound/Egress) 集群的网络流量，特别是应用层的（L7，如 HTTP）流量。

Istio 正在采用这套更先进、更规范的 API 来作为它管理集群外部流量（以及未来的服务网格内部流量）的标准接口。

只有安装了 CRD，Kubernetes 才能识别和存储 Istio 接下来要部署和引用的 Gateway API 资源。

我的理解是相辅相成吧，一个新的概念开始的用原来的架构看不懂，需要定义一个新的api来解释

这条命令是在为您的 Kubernetes 集群“打补丁”，使其能够理解和使用下一代 Kubernetes 流量管理标准——Gateway API。
由于网络问题我不能再终端直接下载github,就使用
先下载，接着再运行yaml文件的形式

<img width="1628" height="296" alt="image" src="https://github.com/user-attachments/assets/d1ce1bb2-7748-4fcb-929a-279e34995d2f" />


（4）再然后，部署示例应用程序
部署 Bookinfo 示例应用程序 ：
kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
<img width="1946" height="564" alt="image" src="https://github.com/user-attachments/assets/ef2b84e7-8bf9-46ab-8977-b5bf67700cd7" />

应用程序将启动。当每个 Pod 准备就绪时，Istio Sidecar 将随之部署。
<img width="1407" height="272" alt="image" src="https://github.com/user-attachments/assets/02def5a2-a3e2-4110-921e-64d767db34ef" />

kubectl get pods

我这里比较慢的原因是没有下载好，要等一会
<img width="1348" height="312" alt="image" src="https://github.com/user-attachments/assets/d1e5c29c-386f-4985-a6b7-d5309fd52ae5" />

<img width="1304" height="355" alt="image" src="https://github.com/user-attachments/assets/7f857d3e-4966-4606-9aea-a588b27c6cc6" />





第二个任务：向外部流量开放应用程序

目的：Bookinfo 应用已部署，但无法从外部访问。为了使其可访问，您需要创建一个入口网关，它将路径映射到网格边缘的路由

（1）首先，为 Bookinfo 应用程序创建 Kubernetes 网关

kubectl annotate gateway bookinfo-gateway networking.istio.io/service-type=ClusterIP --namespace=default

（2）这里要等待镜像拉取，还没好
kubectl port-forward svc/bookinfo-gateway-istio 8080:80




（3）查看仪表板
Istio 与多种不同的遥测应用程序集成。这些应用程序可以帮助您了解服务网格的结构、显示网格的拓扑结构以及分析网格的健康状况。
按照以下说明部署 Kiali 仪表板以及 Prometheus 、 Grafana 和 Jaeger 。


Install Kiali and the other addons and wait for them to be deployed.
访问 Kiali 仪表板。
















