## Pod
Pod is the smallest and simplest unit in which you can run a container. It's like a tiny environment where your application or service runs. Pods are the basic building blocks of your applications in a Kubernetes cluster.

1. **Pod can have one or more containers, but one Pod, one container is recommended**
    While a Pod can indeed have more than one container, it is generally recommended to follow the principle of having a single container per Pod. This approach is easier to manage and      aligns with the concept of a Pod as the smallest deployable unit. Using multiple containers within a Pod is typically reserved for specific use cases, such as sidecar containers or      helper containers that share the same network namespace.
2. **Pods do not have their own IP address**
   Pods within a Kubernetes cluster do not have individual, static IP addresses. Instead, they are assigned a unique IP address within the cluster's network. This IP address is     
   typically reachable only from within the cluster itself. To enable external access to the services or applications running in Pods, you would typically use Kubernetes Services, which    provide a stable IP address and routing capabilities for Pods. The actual IP address assigned to a Pod may change if the Pod is rescheduled or restarted.   

**Imagine a Pod as a single shipping container:**

In the real world, shipping containers hold various goods. Similarly, a Kubernetes Pod holds a single instance of your application, along with its associated data.

***Example:***

Suppose you have a website, and you want to run it on Kubernetes. To do this, you create a Pod for your web server. This Pod can contain just one container, which holds your website's code and serves web pages.

Now, let's say you want to add a database to your website. You would create another Pod, but this time it contains a container with the database software. Your website's code (in the first Pod) can communicate with the database (in the second Pod) to store and retrieve data.

So, in simple terms, a Pod is like a small, isolated environment for your application to run, and you can have multiple Pods working together to create a complete application. Kubernetes takes care of scheduling and managing these Pods, ensuring your application runs smoothly and can be scaled as needed.

**Create pod using imperative command**
```
kubectl run pod-1 --image=nginx
kubectl get pods
```
**Create pod using yaml file**
```
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    app: my-app
spec:
  containers:
  - name: my-container
    image: nginx:latest
    ports:
    - containerPort: 80
```
```
kubectl apply -f pod.yaml
kubectl get pods
```
