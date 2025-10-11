### 1.Orchestration tools, such as Kubernetes, play a key role in the server infrastructure for the modern applications.
(a) How Kubernetes Helps Manage and Scale Application Servers   
Kubernetes helps manage and scale application servers through the following mechanisms:  
1.1 ​​Automated Operations​​:  
Automatically handles Pod deployment, scaling, failure recovery, and rolling updates  
​​1.2 Resource Management​​:  
Precisely controls CPU and memory resource allocation through Requests and Limits  
​​1.3 Elastic Scaling​​:  
Supports Horizontal Pod Autoscaler (HPA) to dynamically adjust replica count based on load  
​​1.4 Load Balancing​​:  
Built-in service discovery and load balancing ensures proper traffic distribution  
​​1.5 Self-healing Capability​​:
Automatically detects and replaces unhealthy containers to ensure high availability  
(b) How Orchestration Tools Facilitate Automation  
Orchestration tools enable automation through:  
2.1 ​​Declarative Configuration​​  
Uses YAML files to define desired state, with the system automatically maintaining that state  
​​2.2 Rolling Updates​​  
Gradually replaces old Pod versions with new ones for zero-downtime deployments  
​​2.3 Blue-Green Deployment​​  
Runs both old and new versions simultaneously for fast switching and rollback  
​​2.4 Auto-scaling​​  
Automatically adjusts replica count based on resource utilization or custom metrics  
​​2.5 Configuration Management​​  
Centralized management of configurations and sensitive information through ConfigMap and Secret  
### 2.Explain the difference between a Pod, Deployment, and Service.
| Resource Type | Purpose | Lifecycle | Use Cases |
| :--- | :--- | :--- | :--- |
| **Pod** | Smallest deployable unit, contains one or more containers | Ephemeral, IP address may change | Running application containers |
| **Deployment** | Manages Pod replicasets, provides update and rollback capabilities | Long-lived, manages Pod lifecycle | Stateless application deployment |
| **Service** | Provides stable network endpoint and service discovery | Long-lived | Service exposure and load balancing |


### 3.What is a Namespace in Kubernetes? Please list one example.
A **Namespace** is a mechanism in Kubernetes for logical resource isolation, used to create virtual working environments within the same physical cluster.  
​​ 
Example​​:

apiVersion: v1  
kind: Namespace  
metadata:
  name: production
​​Use Cases​​:

Environment isolation: development, staging, production  
Team isolation: team-a, team-b  
Project management: project-x, project-y  


### 4. Explain the role of the Kubelet. How do you check the nodes in a Kubernetes cluster? (kubectl command expected)
4.1​​ Kubelet Role​​:  
Agent component running on each worker node  
Responsible for Pod lifecycle management  
Reports node and Pod status to API Server  
Performs container health checks  
​​Node Inspection Commands​​:  
4.2 Commands to check the nodes   
(a)View all nodes  
kubectl get nodes  
(b)View detailed node information  
kubectl describe node <node-name>  
(c)Check node resource usage  
kubectl top nodes  

### 5.What is the difference between ClusterIP, NodePort, and LoadBalancer services?
| Service Type | Access Scope | Typical Use Cases | Example Configuration |
| :--- | :--- | :--- | :--- |
| **ClusterIP** | Cluster-internal only | Internal service communication | type: ClusterIP |
| **NodePort** | NodeIP:Port | Development and testing | type: NodePort |
| **LoadBalancer** | Public internet access | Cloud production deployment | type: LoadBalancer |

---

### 6. How do you scale a Deployment to 5 replicas using kubectl?
#### Method 1: Direct scaling
kubectl scale deployment/my-app --replicas=5

#### Method 2: Edit deployment
kubectl edit deployment my-app
#### Modify replicas field to 5 and save

#### Method 3: Apply updated configuration file
kubectl apply -f deployment.yaml


### 7.  How would you update the image of a Deployment without downtime?
#### Method 1: set image command
kubectl set image deployment/my-app nginx=nginx:1.21

#### Method 2: Edit deployment directly
kubectl edit deployment my-app
#### Update image field and save

#### Method 3: Apply updated file
kubectl apply -f deployment.yaml

#### Check rollout status
kubectl rollout status deployment/my-app

#### Rollback to previous version (if needed)
kubectl rollout undo deployment/my-app


### 8.How do you expose a Deployment to external traffic?
The fundamental issue is how to enable users or systems outside the cluster to securely and reliably access application services running within the Kubernetes cluster. ​
The current situation is that Kubernetes has its own IP address internally, which can only be routed within the cluster network and cannot be directly accessed by external networks. The goal now is to expose this to the outside world.Below are the difficulties encountered during the process and their solutions.

| Challenge | Description | Solution Requirements |
|-----------|-------------|----------------------|
| **Discovery & Addressing** | External clients need to know which IP and port to connect to for accessing the service. | Provides a **stable, reliable external endpoint** (fixed IP/domain) that persists despite Pod restarts or rescheduling. |
| **Load Balancing** | Deployments typically have multiple Pod replicas distributed across nodes - traffic needs even distribution. | Includes **built-in load balancing** to automatically distribute requests across healthy Pod instances. |
| **Network Address Translation (NAT)** | External networks cannot directly route to Pod internal IP addresses. | Implements **network translation** to map external IP:port to internal Pod IP:port. |
| **Security Control** | Service exposure must not compromise security - access needs proper controls. | Provides security layers: **TLS/SSL encryption**, **path/domain-based routing**, **access whitelists**, and other protections. |
| **Production Readiness** | Solution must support high availability, scalability, and manageability for production use. | Supports **zero-downtime updates**, **health checking**, **monitoring integration**, and production-grade reliability. |

**Ingress is a recommended usage method**
#### ​​Method: Ingress (Recommended for Production)​​
Ingress is a Kubernetes API object that manages ​​external access​​ to services within a cluster, typically HTTP/HTTPS traffic. It provides ​​L7 (application layer)​​ routing capabilities, unlike Services which operate at L4 (transport layer).  

Before using Ingress, you must have an ​​Ingress Controller​​ running in your cluster. Common options include:
Nginx Ingress Controller ,Traefik, HAProxy,Istio Ingress ,AWS ALB Ingress Controller.
Define routing rules in an Ingress manifest
Apply the Ingress Configuration



### 9.How does Kubernetes scheduling decide which node a Pod runs on?
The scheduler determines Pod placement based on:  

​​Resource Requirements​​: CPU and memory requests must be satisfied  
​​Node Selectors​​: Match node labels  
​​Affinity/Anti-affinity​​:  
Node affinity: Preference for scheduling on specific nodes  
Pod affinity: Preference for co-scheduling with certain Pods  
Pod anti-affinity: Avoidance of co-scheduling with certain Pods  
​​Taints and Tolerations​​: Control which Pods can schedule onto specific nodes  
​​Resource Constraints​​: Node resource capacity and availability  


### 10.What is the role of Ingress and how does it differ from a Service?
Ingress Role
- **L7 (HTTP/HTTPS) Traffic Management** - Handles application-layer routing and load balancing
- **Advanced Routing** - Supports domain-based (`host: example.com`) and path-based (`path: /api`) routing
- **SSL/TLS Termination** - Provides native HTTPS support with certificate management
- **Virtual Hosting** - Enables multiple domains/services on a single IP
- **Requires Ingress Controller** - Must deploy a controller (e.g., Nginx, Traefik) to implement the rules


#### Ingress vs Service Comparison

| Feature | Service | Ingress |
|---------|---------|---------|
| **Network Layer** | L4 (TCP/UDP) | L7 (HTTP/HTTPS) |
| **Routing Capability** | Port-based only | Domain + path-based |
| **SSL Support** | Requires manual setup | Native termination support |
| **External Access** | Limited (NodePort/LoadBalancer) | Advanced rules via Controller |
| **Primary Use Case** | Internal service communication | External traffic management |

#### Architecture Flow
External Users → Ingress Controller → Service → Pods
