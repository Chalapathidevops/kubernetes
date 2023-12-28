# How does a NodePort Service work ??

![image](https://github.com/Chalapathidevops/kubernetes/assets/145283206/d84fe331-ef0e-4eb0-8341-d67aedfb9bdd)

Let us try to understand the scenario shown in the above diagram.

* There is a worker node which contains a POD in it.
* The POD runs a web application on it.
* There is a NodePort service which we have created and that service, maps the port on the node to a port present on the node.

Now whenever an end user wants to access the web application running on the POD, following things happen behind the scenes

* The user just send request on the Node port number which is mapped to the POD (Here port : 30008)
* Next the NodePort service takes that user request and maps it to its own port i.e service port (Here port : 80)
* Next from the service port, the request is being mapped to the port of the web application POD (Here TargetPort : 80)

**Create a NodePort service**

```
apiVersion: v1 
kind: Service
metadata:  
 name: my-service 
spec:  
 type: NodePort   
 selector:    
  app: echo-hostname    
 ports:
  - nodePort: 30008
    port: 80
    targetPort: 80
```
