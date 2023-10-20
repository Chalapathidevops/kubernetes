## CKA Exam Question
Create a pod named kuccl with a single app container for each of the following images running inside 
there may be between 1 and 4 images specified (nginx-radis-memcached-consul)

**Ans**

```
apiVersion: v1
kind: Pod
metadata:
  name: kuccl
spec:
  containers:
  - name: nginx
    image: nginx
  - name: radis
    image: radis
  - name: memcached
    image: memcached
  - name: consul
    image: consul
```
