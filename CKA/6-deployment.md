
## CKA Exam Question
Reconfigure the existing deployment front-end and add a port specification named http existing port 80/tcp of the existing container nginx
* Create a new service name front-end-svc exposing the container port http
* Configure the new service  to also expose the individual pods via NodePort on the nodes on which they are scheduled.

**Ans:**

**Note:** This deployment already created in Exam, Just we need to edit the deployment and add container port name, and expose it

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

```kubectl expose deploy front-end --name front-end-svc --port 80 --type NodePort --protocal TCP```     
