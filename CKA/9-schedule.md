## CKA Exam Question
Schedule a pod as follows <br>
&emsp; Name: nginx-kusc00401 <br>
&emsp; Image: ngix <br>
&emsp; Node Selector: disk=spinning <br>

***Ans***

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-kusc00401
spec:
  nodeSelector:
    disk: spinning
  containers:
  - name: nginx
    image: nginx
```
