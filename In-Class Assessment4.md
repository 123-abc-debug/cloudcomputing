1. What problem does serverless computing aim to solve compared to traditional microservice deployment on Kubernetes? Give one example where serverless is clearly better, and one where it may not be.

2. What are the advantages of using a service mesh (like Istio) for managing microservices communication instead of relying only on Kubernetes networking?

3. Explain what a sidecar proxy (such as Envoy in Istio) does. Why is it needed in a service mesh?

4. What kind of traffic management features does Istio provide? Give two examples of how they can be useful in production systems.

5. Explain how Knative Serving enables autoscaling for an application. What triggers scaling up and scaling down?

6. What is the role of Knative Eventing, and how does it support event-driven architectures?

7. How does Knative leverage Kubernetes primitives to provide a serverless experience? Discuss which components of Kubernetes (e.g., Deployments, Services, Horizontal Pod Autoscaler) are abstracted away and how this abstraction benefits developers.

8. In KServe, what is the main function of an InferenceService, and how does it simplify deploying ML models?

9. In a production ML workflow using KServe, describe how data moves from an incoming HTTP request to a model prediction response. Which layers (Knative, Istio, KServe, Kubernetes) handle which responsibilities, and where could latency bottlenecks occur?

10. How can Istio鈥檚 traffic routing capabilities (e.g., weighted routing, retries, circuit breaking) be used to support canary deployments or A/B testing in Knative or KServe environments? Discuss the pros and cons compared to manual rollout strategies.


