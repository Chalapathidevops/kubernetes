# What is a LoadBalancer Service 

Imagine a scenario where following has been done :

* You have used NodePort service to expose the application running on POD to the Worker node’s port.
* Now let us assume there are 100 pods running the same application across different worker nodes.
* Each worker node has different ip address. So the URL to access on each node will differ even if the port is same.

So when giving the user endpoint, which node’s URL will you give and how many URLs will you give. Ultimately this will result into a mess.

**Now to solve the above problem, we create a LoadBalancer service.**

Which in simple terms, exposes the whole application by giving user just one URL. And above this, it uses some cloud provider’s (gcp, azure, aws etc) load balancer to balance the user requests to the PODs who are running these services.

In this simple way, By using the LoadBalancer services. User requests can be easily load balanced and the whole application can be exposed using a single URL to the end user.

**Create LoadBalancer**

```
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: LoadBalancer
  selector:
    app: front-end
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
```
