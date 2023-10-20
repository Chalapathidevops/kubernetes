## Pod
Pod is the smallest and simplest unit in which you can run a container. It's like a tiny environment where your application or service runs. Pods are the basic building blocks of your applications in a Kubernetes cluster.

**Imagine a Pod as a single shipping container:**

In the real world, shipping containers hold various goods. Similarly, a Kubernetes Pod holds a single instance of your application, along with its associated data.

***Example:***

Suppose you have a website, and you want to run it on Kubernetes. To do this, you create a Pod for your web server. This Pod can contain just one container, which holds your website's code and serves web pages.

Now, let's say you want to add a database to your website. You would create another Pod, but this time it contains a container with the database software. Your website's code (in the first Pod) can communicate with the database (in the second Pod) to store and retrieve data.

So, in simple terms, a Pod is like a small, isolated environment for your application to run, and you can have multiple Pods working together to create a complete application. Kubernetes takes care of scheduling and managing these Pods, ensuring your application runs smoothly and can be scaled as needed.
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
