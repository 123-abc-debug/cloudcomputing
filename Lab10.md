Deploying a Predictive Model with KServe on Minikube
1. Install and configure KServe on a local Kubernetes cluster (Minikube)

2. Deploy a predictive model using a KServe InferenceService

3. Monitor the status of the service and debug common issues

4. Find out how to reach the InferenceService from outside the cluster.

5. Send inference requests and interpret results


Related links:

https://kserve.github.io/website/docs/getting-started/quickstart-guide
https://kserve.github.io/website/docs/getting-started/predictive-first-isvc
https://futurelei.com/KServe.mov

You are free to choose your own predictive model.

Please write a document with screenshots and notes for major steps and commit it to your github repo.

标题：​​ 在 Minikube 上使用 KServe 部署预测模型完整指南
​​实验环境准备​​
软件版本说明（Minikube, kubectl, helm 等）。
启动 Minikube 集群的命令和截图（例如 minikube start --cpus=4 --memory=8g --disk-size=50g）。
验证集群状态的截图 (kubectl get nodes)。
​​安装 KServe（遵循链接1的 Quickstart Guide，但适配 Minikube）​​
执行 Quickstart 安装脚本的命令和输出截图。
使用 kubectl get pods -n kserve验证安装成功的截图。
可能遇到的问题记录：例如，如果 Pod 状态不是 Running，如何查看日志 (kubectl logs ...) 进行调试。
​​部署预测模型（遵循链接2的指南，选择自己的模型）​​
创建命名空间 kserve-test的截图。
创建 InferenceServiceYAML 文件的内容（可以选用链接中的 sklearn-iris模型，或自行选择其他模型）。
应用 YAML 文件的命令和截图。
监控服务状态直至 READY为 True的截图序列 (kubectl get inferenceservice sklearn-iris -n kserve-test --watch)。
​​确定访问方式（Minikube 环境下的关键步骤）​​
说明 Minikube 没有外部 IP，因此使用 minikube ip和 NodePort。
执行命令查询 istio-ingressgateway的 NodePort 的截图 (kubectl get svc -n istio-system istio-ingressgateway)。
设置 INGRESS_HOST和 INGRESS_PORT环境变量的命令。
​​发送推理请求并解释结果​​
创建 iris-input.json请求文件的截图。
使用 curl命令发送推理请求的命令和输出截图。
对返回结果 {"predictions": [1, 1]}的解释说明。
​​（可选）性能测试与清理​​
运行性能测试 Job 的步骤和结果截图。
实验完成后，清理资源的命令（如 kubectl delete ns kserve-test）。





