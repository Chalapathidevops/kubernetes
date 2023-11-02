## Deployment
  Deployment in Kubernetes is a way to manage and control the rollout of applications and updates in a consistent and automated manner. 
  It ensures that your applications are running smoothly and are easily scalable. 
  A Kubernetes deployment defines the desired state of your application, and Kubernetes takes care of making sure the actual state matches the desired state. 
  If there are any issues or changes needed, Kubernetes automatically handles them, making it easier to manage and maintain your applications. 

  * We can upgrade application from V1 to V2
  * Upgrade with zero downtime
  * Pause and resume upgrade process
  * Rollback upgrade to previous stable version

  * Every deployment one ReplicaSet will create, and this ReplicaSet will pointing to latest one.
  * When we create deployment, by default it will create RS -> Pod -> Container

***Example***

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

## CKA Exam Question
Reconfigure the existing deployment front-end and add a port specification named http existing port 80/tcp of the existing container nginx
* Create a new service name front-end-svc exposing the container port http
* Configure the new service  to also expose the individual pods via NodePort on the nodes on which they are scheduled.

**Ans:**

**Note:** This deployment already created in Exam, Just we need to add the name of the container

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: front-end
  labels:
    app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

**Edit the deployment and add name of the container as "http"** (***Note: This should come under ports section***)

```
kubectl edit deploy front-end
          ports:
          - containerPort: 80
            name: http
```
**Expose**

```kubectl expose deploy front-end --name front-end-svc --port 80 --type NodePort```     