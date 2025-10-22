This lab exercise will give you hands-on experience with Knative for
building, deploying, and managing serverless, cloud-native applications on Kubernetes.

For the following three topics, please submit a word or pdf document containing your compiled screenshots for the key steps.  

[Knative Functions]
https://knative.dev/docs/getting-started/about-knative-functions/

（1）首先，了解knative的好处
Knative Functions 不是 Kubernetes 的替代品，而是它的一个​​“用户体验增强层”​​。它使得在强大的 Kubernetes 平台上运行事件驱动的函数变得像在公有云上使用 AWS Lambda 或 Google Cloud Functions 一样简单，同时保留了私有化部署的灵活性和控制力。
kantive我的理解就是在kubernete上安装了一个平台
kantive func 一个​​命令行工具（funcCLI）​​ 和一套​​开发体验​​。它本身不是一个需要“安装”的独立平台。
​​它的作用​​：它利用Knative Serving的能力，但​​向开发者隐藏了所有复杂性​​。您不需要直接与Knative或Kubernetes交互，只需要使用 func命令。

（2）开始使用knative

你的 Kubernetes 集群上必须已安装 Knative。

已安装 funcCLI​​：这是 Knative Functions 的核心命令行工具。

似乎安装kantive比较麻烦，现在先打算只安装关于func
的部分

为了让你的函数能够通过 URL 被访问，你需要配置 DNS。对于测试环境，最简单的方法是配置 Magic DNS 或直接使用 IP。
就是把github上面的拉取下来



Comments: 1. Use local registry;  2. Skip the "Deploying a function" part

[Knative Serving]
https://knative.dev/docs/getting-started/first-service/

# 部署 Knative 服务
在本教程中，您将部署一个“Hello world”Knative 服务，该服务接受环境变量 TARGET 并打印 Hello ${TARGET}! 。






[Knative Eventing]
https://knative.dev/docs/getting-started/getting-started-eventing/

